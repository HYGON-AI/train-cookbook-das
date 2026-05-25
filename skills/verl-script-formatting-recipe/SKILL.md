---
name: script-formatting-recipe
description: Convention for formatting verl recipe shell scripts — parameter grouping, bash arrays, section headers
---

When reformatting messy verl recipe scripts (or writing new ones), follow this convention strictly. The reference template is [run_qwen3_vl_8b_fsdp2.sh](http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_verl/-/blob/main/examples/recipe/run_qwen2_5_7b_fsdp2.sh).

**Why:** User wants consistent, readable scripts with logical grouping. Messy flat parameter lists are hard to maintain.

**Rules:**

1. **Standard preamble**: Every script MUST start with this exact preamble block after the shebang and `set -xeuo pipefail` (if used). 

   ```
   #!/bin/bash
   for para in $*
   do  
       if [[ $para == --data_path* ]];then
           data_path=${para#*=}
       elif [[ $para == --host_file* ]];then
           host_file=${para#*=}
       elif [[ $para == --hf_model_path* ]];then
           hf_model_path=${para#*=}
       elif [[ $para == --mcore_model_path* ]];then
           mcore_model_path=${para#*=}
       elif [[ $para == --save_ckpt_path* ]];then
           save_ckpt_path=${para#*=}
       elif [[ $para == --profiling* ]];then
           profiling=${para#*=}
       fi
   done

   CURRENT_DIR=$( cd $( dirname $0 ) && pwd )
   VERL_PATH=$( dirname $( dirname ${CURRENT_DIR}))
   NNODES=$( (awk '{print $1}' ${host_file} | sort -u | wc -l) || echo 1 )
   ```

2. **Variable extraction**: Every literal value becomes a variable defined before its array. Compute derived values (e.g., `$((a + b))`) as variables too.

3. **Section headers**: Group by category using `# ===================================== Name =====================================`. Standard categories:
   - Rollout Engine (mode, engine name, async flags)
   - Data (files, lengths, batch sizes)
   - Actor Model & Optim (LR, megatron/fsdp, KL, dynamic bsz)
   - Ref Config (log prob settings, megatron/fsdp for ref)
   - Rollout Config (generation params: n, temperature, top_p, top_k, GPU memory, TP)
   - Algorithm (adv_estimator, KL settings)
   - Reward Config (reward_manager, reward_kwargs)
   - Critic Config (strategy)
   - Trainer (logger, project_name, exp_name, epochs, nnodes, n_gpus, default_local_dir)
   - Async Training (staleness, trigger_sync, partial_rollout)
   - NCCL Config (nccl_timeout — standalone params that don't fit other sections)
   - Profiler Config (torch profiler settings)

4. **Bash arrays**: Each section's params go in a `*_CONFIG=(...)` array. One param per line, 4-space indent. Variables referenced with `${var}` syntax. Hydra `+` prefix preserved for overrides.

5. **Final command**: `python -m ...` with `--config-path`, `--config-name`, `hydra.searchpath`, then `${ARRAY[@]}` expansions. The `hydra.searchpath=[file://${VERL_PATH}/verl/verl/trainer/config]` line MUST be included as the first argument after `--config-name`:

   ```
   python3 -m <module> \
       --config-path=config \
       --config-name='name.yaml' \
       hydra.searchpath=[file://${VERL_PATH}/verl/verl/trainer/config] \
       ${DATA_CONFIG[@]} \
       ...
   ```

6. **Naming conventions**:
   - Array names: UPPERCASE with `_CONFIG` suffix (e.g., `DATA_CONFIG`, `ACTOR_CONFIG`)
   - Variable names: snake_case (e.g., `train_prompt_bsz`, `n_resp_per_prompt`)
   - Path variables end in `_path` (e.g., `train_path`, `hf_model_path`)

7. **Path prefixes**: The following variables MUST use path prefixes from the preamble:
   - `train_file` and `test_file` MUST be prefixed with `${data_path}/`:
     ```
     train_file=${data_path}/dapo-math-17k.parquet
     test_file=${data_path}/aime-2024.parquet
     ```
   - `model_path` MUST be prefixed with `${hf_model_path}/`:
     ```
     model_path=${hf_model_path}/Qwen3-30B-A3B
     ```
   - `trainer.default_local_dir` MUST use `${save_ckpt_path}/ckpts/${project_name}/${exp_name}`:
     ```
     trainer.default_local_dir=${save_ckpt_path}/ckpts/${project_name}/${exp_name}
     ```

8. **Project and experiment names**: Every script MUST define `project_name` and `exp_name` in the Trainer section. If the original script doesn't have them, auto-generate following this pattern:
   ```
   project_name='RECIPE-<MODEL>-DAPO-AIME'
   exp_name='RECIPE-<MODEL>-vLLM'
   ```
   where `<MODEL>` is derived from the model path (e.g., `Qwen3-30B-A3B` → `Qwen3-30B-A3B`). These go in the Trainer section before `TRAINER_CONFIG`.

9. **Standard Profiler Config**: The following block MUST be the last section before the python command. Place it after all other config arrays but before the final python invocation:

   ```
   # ===================================== Profiler Config =====================================
   PROFILE_CONFIG=(
       actor_rollout_ref.actor.profiler.enable=True
       actor_rollout_ref.actor.profiler.ranks=[0,4]
       actor_rollout_ref.actor.profiler.all_ranks=False 
       actor_rollout_ref.actor.profiler.tool_config.torch.contents=['cuda','cpu']
       actor_rollout_ref.ref.profiler.enable=True
       actor_rollout_ref.ref.profiler.ranks=[0,4]
       actor_rollout_ref.ref.profiler.all_ranks=False
       actor_rollout_ref.ref.profiler.tool_config.torch.contents=['cuda','cpu']
       global_profiler.tool=${profiling}
       global_profiler.steps=[3]
       global_profiler.save_path=${VERL_PATH}/examples/grpo_trainer/torch_prof
   )

   # Conditionally Add Torch Profiling Configuration
   if [[ $profiling == "torch" ]]; then
       TRAINER_CONFIG+=(${PROFILE_CONFIG[@]})
   fi
   ```

**How to apply:** When given a messy verl script, extract all parameters, categorize them, pull out literals as variables, and rewrite in this grouped array format.
