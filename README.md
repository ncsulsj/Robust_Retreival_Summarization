# Towards a Robust Retrieval-Based Summarization System

Welcome to the official repository for **Towards a Robust Retrieval-Based Summarization System**. This repository hosts the original implementation of our robust system designed to enhance retrieval-based summarization processes.

## Overview

The system is structured into distinct components to streamline the process of generating data, training the model, and evaluating performance. Specifically, it includes:

- **Data Generation**: Utilizing **SummRAG** to create datasets. (See `create_data.py` in `data_generation` directory)
- **Model Training**: Instructions on training the Mistral 7B instruct v0.1 model with LoRA on our curated datasets. (Located in see
  ` train.py` in `model_training` directory)
- **Model Evaluation**: How to assess the model's performance using **LogicSumm**. (see `evaluate_multi_docs.py` and `evaluate_single_doc.py` in `model_validation` directory)

## Contents

1. [Data and Model Weights](#data-and-model-weights)
2. [Model Functionality](#model-functionality)
3. [Example Inference](#example-inference)

## Data and Model Weights

You could access our generated training and test datasets through the supplementary material. Our trained LoRA model weights is larger than 84MB, which exceeds the size limit (It will be also provided if requested). One can reproduce our model weights through the `train.py` in the `model_training` directory by specifying the training data location .

(To generate the synthetic data, you also need to store OPENAI_API_KEY in a `.env` file in the `data_generation` directory)

## Model Functionality

Our model is fine-tuned for various summarization tasks:
1. **Topic-based Text Retrieval and Summarization**: Capable of identifying the relevancy of retrieval text to a user-defined topic (not only the topic but also the subtopic. i.e. ChatGPT application in Finance is not relevant with ChatGPT introduction or application in Education)
2. **Direct Text Summarization**: Offers summarization on user-provided texts without external text retrieval.
3. **Enhanced Summarization with Supplementary Text**: Identifies and integrates relevant supplementary texts with the original content for comprehensive summarization (also takes care of the case of different subtopic). It also can identify information conflict between them.
4. **Multi-documents Summarization**: Efficiently summarizes multiple documents, filtering out irrelevant content for coherent summaries.

## Example Inference

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
