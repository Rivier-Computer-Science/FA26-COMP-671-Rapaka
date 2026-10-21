# Experimental results

Dataset: CSE-CIC-IDS2018; evaluation: held-out source CSV files.

|   Context length |   Transformer precision (macro) |   Transformer recall (macro) |   Transformer F1 (macro) |   Random Forest F1 (same endpoints) |
|-----------------:|--------------------------------:|-----------------------------:|-------------------------:|------------------------------------:|
|               16 |                          0.8571 |                       0.9973 |                   0.9153 |                                 1   |
|               64 |                          0.8333 |                       0.9997 |                   0.8998 |                                 1   |
|              256 |                          0.5    |                       0.5    |                   0.5    |                                 0.5 |

Limitations: source-day distribution shift, possible unseen labels excluded, and unequal endpoint samples across context lengths.
