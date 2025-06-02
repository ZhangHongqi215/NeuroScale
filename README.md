# NeuroScale: Evolutional Scale-Based Protein Language Models Enable Prediction of Neuropeptides

## Table of Contents
1. [Model Overview](#model-overview)
2. [Environment Setup](#environment-setup)
3. [Data Preparation](#data-preparation)
4. [Code Structure and Usage](#code-structure-and-usage)
5. [Training Parameters](#training-parameters)
6. [Usage Example](#usage-example)
7. [FAQ](#faq)
---

## Model Overview
NeuroScale is a multichannel neural network model based on Evolutionary Scale Modeling (ESM), designed specifically for efficient and accurate neuropeptide (NP) prediction. Key advantages include:
- **Multiscale Feature Extraction**: Combines pretrained protein language models (ESM2) and GoogLeNet architecture to capture the complex relationship between sequence, structure, and function.
- **High Robustness**: Maintains stable performance across various protein sequence similarity thresholds and sequence lengths.
- **Efficient Computation**: Single inference time of less than 0.035 seconds, suitable for large-scale data.

The model has significant applications in neuropeptide-related disease mechanism research and peptide drug development.

---

## Environment Setup
### Hardware Requirements
- GPU: Recommended NVIDIA GPU (e.g., RTX 3090, with ≥24GB VRAM)
- Memory: ≥128GB RAM

### Software Dependencies
- Python 3.8+
- Key Libraries:
  ```bash
  pip install torch transformers biopython scikit-learn nltk gensim
  ```


## Data Preparation

### Data Format

Input data: FASTA format files containing both positive samples (neuropeptides) and negative samples (non-neuropeptides).

Example file structure:
```bash
NP_001 MKLFVPLLL... 
NP_002 GGVGSAALAM...
```
### Data Preprocessing

- **Length Filtering:** Retain sequences with lengths between 5–100.
- **Redundancy Removal:** Use CD-HIT (v4.8.1) to remove sequences with >80% similarity.
- **Balanced Dataset:** Ensure the number of positive and negative samples is balanced.

### Data Path Configuration

Modify the file paths in the code:

```python
p = getFastaData('path/to/pos4.fasta')  # Positive sample path
n = getFastaData('path/to/nes4.fasta')  # Negative sample path

```
## Code Structure and Usage
### Key Code Modules
- **Data Loading:** The getFastaData function parses the FASTA file and extracts sequences.
- **Model Definition:** The myModel class integrates the ESM2 feature extractor and multichannel fully connected network.
- **Training Loop:** Five-fold cross-validation, with SGD optimizer.
- **Evaluation Metrics:** The comp_result function calculates accuracy, F1 score, AUC, and other metrics.


## Training Parameters
- **Learning Rate:** 0.001
- **Batch Size:** 1 (can be adjusted, but memory limits should be considered)
- **Optimizer:** SGD

## Usage Example
### Quick Start
- **Clone the repository:**
```base
git clone https://github.com/ZhangHongqi215/NeuroScale
```
- **Replace Data Paths**
- **Run Jupyter Notebook:**
```base
jupyter notebook NeuroScale.ipynb
```
## FAQ

- **CUDA Out of Memory:** Reduce the batch size or use a smaller ESM2 model.
- **Incorrect Data Path:** Ensure the FASTA file path is correct and the file is readable.
- **Dependency Conflicts:** Use a virtual environment (e.g., conda) to isolate Python dependencies.
