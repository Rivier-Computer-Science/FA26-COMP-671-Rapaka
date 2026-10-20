# Adversary Behavior Classification from Sequential Logs

## 1. Project Overview

This project investigates the use of deep learning to classify cybersecurity behaviors from sequential network activity. The goal is to determine whether a model can learn meaningful patterns from sequences of network events and distinguish benign traffic from malicious activity.

Traditional intrusion detection systems often rely on predefined rules and signatures. Although these methods are useful, they may struggle with unfamiliar or complex attack patterns. This project explores whether a Transformer-based model can use the temporal context of network events to improve classification.

The project uses the CIC-IDS2017 dataset, which contains labeled benign and malicious network-flow records.

**Project type:** Deep Learning / Cybersecurity  
**Programming language:** Python  
**Deep learning framework:** PyTorch  
**Development environment:** Visual Studio Code  
**Version control:** Git and GitHub

## 2. Research Question

**How does the amount of historical network-event context affect the performance of a Transformer-based cybersecurity classification model?**

The project investigates whether increasing the sequence context improves classification performance and whether the Transformer performs better than a simpler baseline model.

## 3. Project Objectives

- Prepare and analyze labeled cybersecurity network-flow data.
- Develop a baseline classification model for comparison.
- Implement a Transformer-based sequence classification model.
- Compare sequence lengths of 16, 64, and 256 events.
- Evaluate performance using precision, recall, macro-F1, and confusion matrices.
- Analyze classification errors and limitations.
- Document the complete workflow so that experiments can be reproduced.

## 4. Dataset

The project uses the **CIC-IDS2017 Intrusion Detection Evaluation Dataset**, published by the Canadian Institute for Cybersecurity at the University of New Brunswick.

Official dataset website: https://www.unb.ca/cic/datasets/ids-2017.html

The dataset includes labeled network flows representing benign traffic and several types of simulated cyberattacks.

The dataset will be downloaded separately and will not be committed to this repository because of its size.

### Data Preparation

The preprocessing pipeline will:

1. Load the downloaded CSV files.
2. Standardize column names and inspect the available labels.
3. Handle missing values, infinite values, and duplicate records where appropriate.
4. Encode categorical labels and prepare numerical features.
5. Preserve timestamps and sequence ordering where the available data supports it.
6. Split data into training, validation, and test sets.
7. Construct sequences for the different context-window experiments.

To prevent data leakage, preprocessing parameters will be learned from the training data only. The final test set will remain separate from model selection and tuning.

The exact split strategy and label definitions will be documented after inspecting the dataset.

**Dataset limitation:** CIC-IDS2017 contains network-flow records, not raw operating-system process logs. Therefore, this project focuses on network-activity classification and does not claim to directly classify process-level adversary behavior.

## 5. Methodology

### 5.1 Baseline Model

A simpler model using TF-IDF or aggregated network-flow features will serve as the baseline. The final baseline representation will be selected after examining the dataset structure.

This baseline provides a reference for determining whether the Transformer offers a meaningful improvement.

### 5.2 Transformer Model

A Transformer-based sequence classifier will process ordered network-event representations. Self-attention allows the model to learn relationships between events within a sequence.

The model will be implemented using PyTorch. Its architecture and hyperparameters will be documented in the source code and experiment configuration.

### 5.3 Controlled Comparison

The main experiment will compare three context-window sizes:

- 16 events
- 64 events
- 256 events

This experiment investigates whether longer historical context improves classification performance. Model settings and data-splitting rules will be held consistent wherever practical.

## 6. Evaluation Metrics

The following metrics will be used:

- **Precision:** How many predicted examples of a class are correct?
- **Recall:** How many actual examples of a class are detected?
- **Macro-F1:** How well does the model perform across classes, giving each class equal weight?
- **Confusion matrix:** Which classes are confused with one another?

Macro-F1 will be a primary comparison metric because cybersecurity datasets can contain substantial class imbalance. Recall and false-positive behavior will also be examined.

Results will be reported from actual experiments. No performance improvement will be assumed in advance.

## 7. Project Structure

```text
adversary-behavior-classification/
├── README.md
├── requirements.txt
├── .gitignore
├── configs/
├── data/
├── models/
├── results/
├── report/
├── tests/
└── src/
    └── __init__.py
```

As development progresses, the `src/` directory will contain data-loading, preprocessing, baseline, Transformer, training, and evaluation modules.

The `configs/` directory will contain experiment settings. The `results/` directory will contain selected metrics and figures. The `report/` directory will contain the written report and presentation materials.

## 8. Requirements

- Python 3.11 recommended
- Git
- Visual Studio Code
- A Windows, Linux, or macOS computer
- Sufficient disk space for the dataset
- Internet access to download the dataset and Python packages

The experiments will initially support CPU execution. A compatible GPU may reduce training time but is not required for the initial development workflow.

## 9. Installation

### Step 1: Clone the repository

```bash
git clone https://github.com/YOUR-USERNAME/adversary-behavior-classification.git
cd adversary-behavior-classification
```

Replace `YOUR-USERNAME` with your GitHub username.

### Step 2: Create a virtual environment

On Windows PowerShell:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

If PowerShell blocks activation, run the following command in the current terminal and retry:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
```

### Step 3: Install dependencies

```bash
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

### Step 4: Download the dataset

Download CIC-IDS2017 from the official dataset website and extract the relevant labeled-flow CSV files into the local `data/` directory.

The raw dataset is intentionally excluded from Git tracking.

## 10. Running the Experiments

The training and evaluation commands will be added as the corresponding scripts are implemented.

The intended workflow is:

1. Inspect and preprocess the dataset.
2. Create training, validation, and test partitions.
3. Train the baseline model.
4. Train the Transformer model.
5. Evaluate the context-window experiments.
6. Generate metrics, figures, and failure-analysis examples.

The final commands and configuration options will be documented here once the scripts are implemented and tested.

## 11. Reproducibility

To support reproducible experiments, the project will document:

- Dataset source and label definitions.
- Data preprocessing steps.
- Training, validation, and test split strategy.
- Random seeds where applicable.
- Model architecture and hyperparameters.
- Dependency versions.
- Evaluation metrics and experiment results.

Model checkpoints and generated artifacts will be managed according to their size and the repository's storage requirements.

## 12. Ethics and Responsible Use

This project is intended for academic research and defensive cybersecurity analysis.

The dataset contains simulated attack activity. Classification results should not be interpreted as definitive evidence that a real system is compromised.

Potential limitations include dataset bias, class imbalance, distribution shifts, false positives, and reduced performance on unseen environments. Models may also learn dataset-specific artifacts rather than generalizable attack behavior.

The system is an experimental classifier and should not independently trigger high-impact security actions without further validation and human oversight.

## 13. Expected Deliverables

The final project will include:

- A working data-preprocessing pipeline.
- A baseline classification model.
- A Transformer-based classification model.
- Controlled context-window experiments.
- Evaluation tables, figures, and failure analysis.
- Source code and dependency documentation.
- A reproducible GitHub repository with multiple meaningful commits.
- An 8–12-page written report, excluding references and appendix.
- A project presentation or video.

## 14. Project Status

**Current stage:** Initial repository setup and environment preparation.

Implementation, experimental results, and conclusions will be added as development progresses. Reported performance metrics will reflect completed experiments rather than assumed outcomes.

## 15. References

1. Canadian Institute for Cybersecurity, University of New Brunswick. *CIC-IDS2017 Dataset*. https://www.unb.ca/cic/datasets/ids-2017.html

2. Vaswani, A., et al. (2017). *Attention Is All You Need*. Advances in Neural Information Processing Systems. https://arxiv.org/abs/1706.03762

3. Prince, S. J. D. *Understanding Deep Learning*. MIT Press. https://udlbook.github.io/udlbook/

