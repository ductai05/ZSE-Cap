# ZSE‑Cap

**ZSE‑Cap** (Zero‑Shot Ensemble for Captioning) is a zero‑shot system for **article‑grounded image retrieval** and **prompt‑guided captioning**, developed for the EVENTA 2025 challenge (33rd ACM Multimedia). The approach ranked **Top‑4** on the private test set.

---

## Table of Contents

- [Overview](#overview)  
- [Key Features](#key-features)  
- [System Architecture](#system-architecture)  
- [Evaluation Results](#evaluation-results)  
- [Contributing](#contributing)  
- [License](#license)  
- [Preprint](#preprint)
- [Citation](#citation)  

---

## Overview

ZSE‑Cap addresses two interconnected tasks:

1. **Image Retrieval**  
   Given an article and a query image, retrieve the most relevant images from a large collection (OpenEvents V1, ~400K images).

2. **Caption Generation**  
   Produce an event‑aware, article‑grounded caption for the query image using prompt engineering on a large language model.

Unlike typical approaches, ZSE‑Cap requires **no task‑specific fine‑tuning**—it leverages pre‑trained foundation models in a zero‑shot ensemble.

---

## Key Features

- **Ensemble Retrieval** using multiple vision backbones  
- **Weighted fusion** of CLIP, SigLIP, and DINOv2 embeddings  
- **Prompt‑guided captioning** with Gemma 3 (or your preferred LLM)  
- Fully zero‑shot: no additional training on EVENTA data  

---

## System Architecture

1. **Embedding Extraction**  
   - Compute image embeddings with CLIP, SigLIP, and DINOv2.  
   - Store all database embeddings on disk.

2. **Weighted Ensemble Retrieval**  
   - For a query image, compute L2 distances in each embedding space.  
   - Fuse scores with weights:  
     - DINOv2 – 0.4545  
     - CLIP – 0.2727  
     - SigLIP – 0.2727  
   - Return top‐K candidate images and their associated articles.

3. **Prompt‑Guided Captioning**  
   - Construct a single prompt that includes:  
     1. Query image (or its high‑level description)  
     2. Retrieved article text  
     3. Instruction to produce an event‑focused caption  
   - Call Gemma 3 (or any strong LLM) via API to generate the caption.

---

## Evaluation Results

| Metric (private set)         | Value   |
|------------------------------|--------:|
| Retrieval mAP                | 0.966   |
| Retrieval R@1                | 0.955   |
| Retrieval R@10               | 0.983   |
| Caption CIDEr                | 0.133   |
| Caption CLIPScore            | 0.828   |

Ranked **4th place** out of all submissions on EVENTA 2025.

---

## License

This project is licensed under the **MIT License**. See the [LICENSE](LICENSE) file for details.

---

## Preprint

Available soon...

## Citation

If you use ZSE‑Cap in your research, please cite our paper: Available soon...


