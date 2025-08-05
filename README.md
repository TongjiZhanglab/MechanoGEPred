# MechanoGEPred
![label1](https://img.shields.io/badge/license-MIT-green)

This repository contains a computational model that predicts the elastic modulus of cells based on mechanosensitive genes expression. The model was trained using gradient boosting algorithm and is stored in a joblib format for easy deployment.

## 📦 Repository Structure
```text
MechanoGEPred/
├── data/                       # Datasets and gene lists
│   ├── example_data.csv        # Example input data for prediction
│   ├── mechano_genes_list.txt  # 344 mechanosensitive genes used by model
│   └── train_test_data.csv     # Training and validation dataset
│
├── model/                      # Pretrained models
│   ├── model.joblib            # GradientBoostingRegressor model
│   └── scaler.joblib           # Feature scaler
│
├── notebook/                   # Jupyter notebooks
│   ├── model_training.ipynb    # Model development workflow
│   └── tutorial.ipynb          # Comprehensive usage tutorial
|
|—— output/                     # Predictions output
|   └── TCGA_COAD_predictions.csv # Predictions for TCGA COAD dataset
│
├── LICENSE
├── README.md                   # This documentation
└── requirements.txt            # Python dependencies
```

## 🚀 Quick Start Guide
1. Environment Setup
```bash
# Create and activate conda environment
conda create -n MechanoGEPred python=3.11 -y
conda activate MechanoGEPred

# Install dependencies
pip install -r requirements.txt
```

2. Run Minimal Prediction Example
```python
import joblib
import pandas as pd

# Load model components
model = joblib.load('model/model.joblib')
scaler = joblib.load('model/scaler.joblib')
genes = pd.read_csv('data/mechano_genes_list.txt', header=None)[0].tolist()

# Load and prepare data
data = pd.read_csv('data/example_data.csv', index_col=0)
processed = data.reindex(columns=genes, fill_value=0)
scaled = scaler.transform(processed)

# Make predictions
predictions = model.predict(scaled)
print(f"Predicted modulus values: {predictions}")
```

3. Explore the Tutorial
For comprehensive guidance, open and run the Jupyter notebook: `notebook/tutorial.ipynb`

## Citation
