# FA26-COMP-671-Rapaka
## Adversary Behavior Classification from Sequential Network Flows

A reproducible academic deep-learning project comparing a Random Forest flow baseline with a PyTorch Transformer using event context windows of **16, 64, and 256** flows.

### Dataset: CSE-CIC-IDS2018
Official dataset: https://www.unb.ca/cic/datasets/ids-2018.html

CSE-CIC-IDS2018 is a large, labeled network-flow intrusion-detection dataset (roughly 16 million flows across its collection). It contains benign activity and multiple simulated attacks. **It is network-flow data, not operating-system process logs.** Download the labeled CSV files manually and extract them under `data/raw/`. Raw data is excluded from GitHub.

### Research question
How does historical network-flow context (16, 64, or 256 events) affect the macro-F1 of a Transformer intrusion classifier relative to a simple Random Forest baseline?

### Installation (Windows PowerShell / VS Code)
```powershell
git clone https://github.com/YOUR-USERNAME/YOUR-REPO.git
cd YOUR-REPO
py -3.11 -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -r requirements.txt
python -m ipykernel install --user --name adversary-env --display-name "Python (adversary-env)"
code .
```
If PowerShell blocks activation: `Set-ExecutionPolicy -Scope Process Bypass`.

### Run
1. Download **at least three** labeled CSE-CIC-IDS2018 CSV files and place them in `data/raw/`.
2. Open `notebooks/adversary_behavior_classification.ipynb` in VS Code.
3. Select the `.venv` Python kernel and run cells from top to bottom.
4. Start with `MAX_ROWS_PER_FILE=20000` and `EPOCHS=3`. For a quick check, set `SEQUENCE_LENGTHS=[16]` and `EPOCHS=1`.
5. Review metrics and figures under `results/`; model checkpoints under `models/`.

### Method
- Load CSV files in chunks, clean numeric features, impute/clip/scale using training-only statistics.
- Split by source CSV file into train/validation/test; remove evaluation classes unseen during training and report their counts.
- Train Random Forest on individual flows.
- Construct non-overlapping sequences within files, ordered by timestamp when reliable; classify last event.
- Train Transformer encoder for contexts 16/64/256; select best epoch by validation macro-F1.
- Evaluate precision, recall, macro-F1, classification reports and confusion matrices on test data.
- Compare Random Forest at the same test-window endpoints for a fairer reference.

### Caveats
A CSV file may contain attacks absent from training, and file-disjoint splits may therefore exclude evaluation labels. Temporal adjacency does not prove a shared session or adversary chain. Data artifacts, class imbalance, missing timestamps, and hardware constraints may limit results. Report exclusions and limitations clearly; do not invent metrics. The notebook is a starter implementation, not a pre-validated published benchmark.

### Structure
```text
notebooks/adversary_behavior_classification.ipynb
requirements.txt
README.md
.gitignore
data/raw/ (downloaded CSVs, ignored)
models/ (checkpoints, ignored)
results/ (generated outputs, ignored)
src/
configs/
report/
tests/
```

### Deliverables
Working notebook, baseline and Transformer models, 16/64/256 context experiments, reproducible metrics and confusion matrices, documented limitations, 8–12 page report, presentation, and GitHub commit history.

### References
- Canadian Institute for Cybersecurity, CSE-CIC-IDS2018: https://www.unb.ca/cic/datasets/ids-2018.html
- Vaswani et al. (2017), Attention Is All You Need: https://arxiv.org/abs/1706.03762
- Prince, Understanding Deep Learning: https://udlbook.github.io/udlbook/

## Actual training and experimental scores

Open `notebooks/adversary_behavior_classification.ipynb`, place real CSE-CIC-IDS2018 CSVs in `data/raw/`, and run all cells. The notebook **trains** a Random Forest and three Transformer configurations (16/64/256 events) and computes scores from held-out test files. Results are saved in `results/experiment_metrics.csv`, `results/final_scores.csv`, `results/report_results.md`, and PNG confusion matrices. No scores are invented or prefilled.

For a CPU trial, the default notebook caps each file at 20,000 rows and each split at 1,500 windows. Increase those limits for larger experiments if RAM/compute allow. Be aware that held-out-day splits can contain attack labels absent from training; the notebook reports and excludes such labels from validation/test.
