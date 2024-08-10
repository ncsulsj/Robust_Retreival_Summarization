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
1. **moe_projector.py**: It consists of the implementation of SparseMoE and QFormer projector.
2. **modeling.py**: Main implementation of Guardian by following HuggingFace Model Template. 

## Training job

To utilize our model for different use cases, consider the following prompts:

- **For Topic-based Summarization**:
  ```
  [INST] You are a summarization assistant to retrieve the text based on user's topic and then do the summarization. Hi, could you provide a summary of xxx ? [/INST] Here is the retrieval text: Start of the retrieval text: xxx End of the retrieval text.
  ```
- **For Direct Text Summarization**:
  ```
  [INST] You are a summarization assistant to do the summarization based on user's text. Hi, could you provide a summary of this text regarding xxx? [/INST] 
  ```
  The model usually returns you `Sure, could you provide the text?`. Then you could reply
  ```
  [INST] Your text [/INST] Here is the retrieval text: Start of the retrieval text: xxx End of the retrieval text. 
  ```
- **Enhanced Text Summarization**:
  ```
  [INST] You are a summarization assistant to decide if combining the retrieval text with user's text to do the summarization based on its relevancy. Hi, could you summarize the following text for me?
  Besides, could you also check retrieve some related text and see if it can improve the summarization and also check the information conflict? [/INST]
  ```
  The model usually returns you `Sure, could you provide the text?`. Then you could reply
  ```
  [INST] Your text [/INST] Here is the retrieval text: Start of the retrieval text: xxx End of the retrieval text.
- **Multi-documents Summarization**:
  ```
  Use the function, inference_template_s7, located in model_validation/llm_utils.py, the input argument is user's topic, all the retrieval texts as a python list of string and the lora repo.
  ```
  The above function will directly return you with the final summarization.
