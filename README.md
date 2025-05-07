# Podcast Listening Time Prediction

This repository contains code for predicting podcast listening time using machine learning models. The project is based on a Kaggle dataset and competition focused on predicting how long listeners will engage with podcast episodes.

## Overview

The goal of this project is to predict the `Listening_Time_minutes` for podcast episodes based on various features such as episode length, host popularity, guest popularity, publication time, and more. This prediction helps podcast creators and platforms understand listener engagement patterns.

## Getting Started

### Prerequisites

- Python 3.10+
- Jupyter Notebook
- Required packages:
  - pandas
  - scikit-learn
  - joblib
  - numpy

### Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/podcast-listening-prediction.git
cd podcast-listening-prediction

# Create and activate a virtual environment (recommended)
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### Kaggle CLI Commands

To download the competition data using the Kaggle CLI:

```bash
# Make sure you have your Kaggle API credentials set up in ~/.kaggle/kaggle.json
kaggle competitions download -c predict-podcast-listening-time
unzip predict-podcast-listening-time.zip -d data/
```

## Project Structure

```
├── artifacts/
│   ├── models/                         # Saved model files
│   │   ├── model_random_forest.pkl
│   │   ├── model_xgboost.pkl
│   │   ├── model_lightgbm.pkl
│   │   └── model_catboost.pkl
│   ├── tree_model_results.json        # Results from model evaluation
│   └── podcast_name_cluster_map.json  # Mapping for podcast name clusters
├── data/
│   ├── train.csv                      # Training dataset
│   ├── test.csv                       # Test dataset
│   └── submissions/                   # Model predictions for submission
│       └── submission_1.csv
├── model_inference.ipynb              # Inference notebook
└── README.md                          # This file
```

## Data Processing

The inference pipeline includes several preprocessing steps:

1. **Feature Engineering**:
   - Podcast name clustering and encoding
   - Episode title binning (early: 1-33, mid: 34-66, late: 67-100)
   - One-hot encoding for categorical variables
   - Ordinal encoding for sentiment

2. **Data Cleaning**:
   - Handling missing values in `Episode_Length_minutes` (mean imputation)
   - Handling missing values in `Guest_Popularity_percentage` (mean imputation)

## Model Selection

The project uses tree-based models:
- Random Forest Regressor
- XGBoost
- LightGBM
- CatBoost

The best model (Random Forest Regressor) is selected based on the lowest RMSE on the validation set.

## Making Predictions

To generate predictions for the test set:

1. Open and run the `model_inference.ipynb` notebook
2. The predictions will be saved to `data/submissions/submission_1.csv`

## Model Features

The model uses the following features:

- **Numerical features**:
  - Episode_Length_minutes
  - Host_Popularity_percentage
  - Guest_Popularity_percentage
  - Number_of_Ads

- **Categorical features** (one-hot encoded):
  - Podcast_Name_clustered
  - Episode_Title_binned
  - Genre
  - Publication_Day
  - Publication_Time
  - Episode_Sentiment

## Author

- Finian O'Neill

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgements

- This project is part of a Kaggle competition for predicting podcast listening time
- Thanks to Kaggle for providing the dataset and platform