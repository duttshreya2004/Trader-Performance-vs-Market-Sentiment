# Primetrade.ai — Data Science Intern Assignment
Objective
Analyze how Bitcoin market sentiment (Fear/Greed Index) relates to trader behavior and performance on Hyperliquid, and uncover patterns that could inform smarter trading strategies.

Project Structure
├── fear_greed_index.csv        # Bitcoin Fear/Greed sentiment data (2018–2025)
├── historical_data.csv         # Hyperliquid trader data (211,224 trades)
├── Data_Science_PrimeTrade.ipynb  # Main analysis notebook
├── README.md                   # This file
└── analysis_writeup.md         # Summary of methodology, insights & strategies

Datasets
DatasetRowsColumnsDate Rangefear_greed_index.csv2,64442018-02-01 to 2025-05-02historical_data.csv211,224162023-05-01 to 2025-05-01merged_df (final)~196,854252024-01-01 to 2025-05-01

Setup Instructions
1. Install Required Libraries
bashpip install pandas numpy matplotlib seaborn scipy
2. Place Data Files
Make sure both CSV files are in the same folder as the notebook:
fear_greed_index.csv
historical_data.csv
3. Run the Notebook
Open the notebook and run all cells top to bottom:
bashjupyter notebook Data_Science_PrimeTrade.ipynb
Or in JupyterLab:
bashjupyter lab Data_Science_PrimeTrade.ipynb

How to Run — Step by Step
StepWhat it doesPart A — Q1Loads both datasets, checks missing & duplicate valuesPart A — Q2Converts timestamps, aligns datasets by date, filters to 2024+Part A — Q3Creates key metrics: PnL, win rate, leverage, trade frequency, long/short ratioPart B — Q1Analyzes performance differences on Fear vs Greed daysPart B — Q2Analyzes trader behavior changes based on sentimentPart B — Q3Segments traders into 3 groups and compares performancePart CStrategy recommendations based on findings

Libraries Used
pythonimport pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from scipy import stats
import warnings

Key Findings (Quick Summary)

Traders are more active on Fear days but suffer bigger losses
Infrequent traders earn 2x more than frequent traders
Low leverage outperforms high leverage overall
On Greed days, infrequent + low leverage is the best combination
