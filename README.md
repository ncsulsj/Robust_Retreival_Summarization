# Diffusion Based for Sequence Anomaly Detection

Welcome to the official repository for **Diffusion Based for Sequence Anomaly Detection**. This repository hosts the original implementation of our sequence anomaly detection model.

## Overview

The system is structured into distinct components. Specifically, it includes:

- **TSA_training**: TSA baseline embedding algorithm for modeling the ShipTrack Sequence
- **LLM_SimCSE**: SimCSE algorithm to finetune nomic embedding to adapt to ShipTrack domain
- **DTE**: Diffusion time estimation model training for anomaly detection.


## Contents

1. [TSA training](#TSA-training)
2. [LLM_SimCSE](#LLM-SimCSE)
3. [DTE](#DTE)

## TSA training

This directory includes the code to train the TSA on the ShipTrack sequence through PyTorch Lightning

## LLM_SimCSE

This directory includes the code to use SentenceTransformer to finetune Nomic on the ShipTrack sequence after text transformation.

## DTE

This directory includes the code to train our main anomaly detection algorithm - DTE and other baseline algorithms such as DDPM.
