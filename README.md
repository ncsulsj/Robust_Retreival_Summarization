# Guardian - Unified Multi Modality LLM for Returns Abuse Prevention

Welcome to the official repository for **Guardian**. This repository hosts the original implementation of our unified Multi-Modaltiy LLM for Returns Abuse Prevention.

## Overview

The system is structured into distinct components of Guardian Framework. Specifically, it includes:

- **Synthetic Dialogue Generation**: Utilizing **prompts** together with **Claude 3** to create datasets to help Guardian in SOP understanding, reasoning, robustness, etc... (See `configs` directory for prompts)
- **Model Training**: Training Job to train Guardian. (Located in `Guardian_training_job` directory)


## Contents

1. [Generate synthetic dialogue](#Generate-synthetic-dialogue)
2. [Guardian code structure](#Guardian-code-structure)
3. [Traning job](#training-job)

## How to generate synthetic dialogue

To generate synthetic dialogue to understand SOP, SOP reasoning, robustness, etc.. through Claude 3, all SOPs need to put under `sop_image` folder. After this step, run `generate_image_multiple.py` to automatically parse SOPs into images. Given access to Claude 3 and all arguments, run `data_creation.py` for synthetic dialogue generation.

## Guardian code structure

Guardian has following code structure in `Guardian_training_job/src/Guardian_config_and_code/scripts` directory:
1. `moe_projector.py`: It consists of the implementation of SparseMoE and QFormer projector.
2. `modeling.py`: Main implementation of Guardian by following HuggingFace Model Template. 

## Training job

To train Guardian through training job, one needs to pay attention to following files:

1. `Guardian_training_job/src/Guardian_config_and_code/scripts/run_multinode_deepspeed.py`: This script trains Guardian with QLoRA with Deepspeed stage 3 for single node/multiple nodes.
2. `Guardian_training_job/src/Guardian_config_and_code/scripts/torch_launch.sh`: This shell script file launch Guardian training through  `torchrun` command.
3. `Guardian_training_job/src/start.py`: Entry point for the Guardian Training with specifying certain SageMaker environment variable such as Master Address...
