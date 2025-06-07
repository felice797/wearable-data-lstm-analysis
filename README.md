# Wearable-Based Digital Biomarkers: An LSTM-Powered Progression Index for Parkinson’s Disease Monitoring

**Author**: Felice Dong \
**Advisor**: Dr. Hemant Tagare \
**Department**: Statistics and Data Science, Yale University \
**Completion Date**: April 30, 2025 

## Contents 
1. [Overview](#overview)
2. [Repository Structure](#repository-structure)
3. [Quick Start](#quick-start)
4. [Data](#data)
5. [Model Architecture](#model-architecture)
6. [Methodology](#methodology)
7. [References and Related Work](#references-and-related-work)
8. [Future Directions](#future-directions)
9. [Acknowledgements](#acknowledgements) 

## Overview 

Parkinson's disease (PD) affects over 10 million peopole worldwide, making objective, accessible monitoring crucial for both clinical research and patient care. The current project addresses this by developing a data-driven progression index that: 
- **Leverages wearable sensor data** for continous, remote monitoring of motor symptoms
- **Uses LSTM networks** to capture temporal dependencies in activity patterns
- **Provides objective measurements** that complement subjective clinical scales

#### Key Findings 
- **Visual separation achieved** between PD and healthy control subjects across all evaluation splits
- **Peak activity capability** identified as the most discriminative feature for disease status
- **Weekend activities** showed higher predictive value than weekday routines
- **Sorted activity features** provided more robust discrimination than conventional weekday labels

## Repository Structure 
```
├── src/                           # Source code
│   ├── requirements.txt           # Python dependencies
│   └── lstm_pd_progression.py     # Main LSTM model implementation
│ 
├── data/                          # Dataset files
│   ├── enhanced_fake_data.csv     # Synthetic dataset for demonstration
│   ├── fake_data.csv              # Basic synthetic dataset
│   └── fake_data_generation.ipynb # Data generation notebook
│ 
├── docs/                          # Documentation
│   ├── dong_felice_thesis.pdf     # Complete thesis document
│   └── FD_THESIS_Poster.pdf       # Research poster
│ 
├── notebooks/                     # Analysis notebooks
│   ├── thesis_model_cleaned.ipynb # Thesis model implementation
│   └── lstm_fake_data.ipynb       # Experiments with synthetic data
└── README.md                      # This file
```

## Quick Start 

#### Prerequisites 
- Python 3.8+
- R 4.0+ (for data preprocessing)
- Required Python packages (see `src/requirements.txt`)

#### Installation 

- Clone the repository
  ```
  git clone https://github.com/felice797/wearable_data_lstm_analysis.git
  cd wearable_data_lstm_analysis
  ```
- Install Python dependencies
  ```
  pip install -r src/requirements.txt
  ```
- Run the model
  ```
  python src/lstm_pd_progression.py --data_path data/enhanced_fake_data.csv --output_dir results
  ```

#### Command Line 
```
python src/lstm_pd_progression.py [OPTIONS]

Options:
  --data_path       Path to input CSV file (default: Data_preimp.csv)
  --output_dir      Directory to save results (default: ./results)  
  --num_splits      Number of cross-validation splits (default: 20)
  --seed            Random seed for reproducibility (default: 42)
```
## Data 
CSV with the following required columns: 
- `subject`: Unique subject identifier
- `cohort`: `PD` or `Control`
- `week_num`: Week number
- `Mon`, `Tue`, `Wed`, `Thu`, `Fri`, `Sat`, `Sun`: Daily ambulatory minutes

***Note***: The real PPMI dataset used in the thesis cannot be shared due to data privacy aggreements. Synthetic data is provided for demonstration purposes. 
  
## Model Architecure 
The LSTM-based progression index uses:

- **Input Layer**: 7 features (daily activity minutes)
- **LSTM Layers**: 2 layers with 20 hidden units each
- **Output Laye**r: Linear transformation with normalized weights
- **Custom Loss Function**: Optimizes separation between PD and healthy controls with time weighting

#### Feature Representations

1. **Conventional Weekday Features**: Monday through Sunday activity levels
2. **Sorted Activity Features**: Daily activities ordered by intensity (most to least active)

## Methodology 

#### Data Processing Pipeline 
1. **Quality filtering** for subjects with $\geq$ 26 weeks of data
2. **Missing data interpolation** for gaps $\leq$ 2 days
3. **Feature transformation** to create intuitive progression scale
4. **Temporal alignment** across subjects

#### Model Training 
- **Cross-validation** with 20 independent train-test splits
- **Data augmentation** with Gaussian noise and time swapping
- **Balanced sampling** to address cohort imbalance
- **Early stopping** based on loss convergence

## References and Related Work 
This research builds upon: 

1. **Verily Life Sciences Study** (Chen et al., 2023): Digital biomarkers detected treatment effects earlier and with smaller sample sizes than traditional clinical assessments in Lewy Body Dementia patients.
2. **PPMI Database**: Longitudinal study providing wearable sensor data from PD patients and healthy controls.
3. **LSTM Networks**: Effective for capturing long-term temporal dependencies in time series data.

## Future Directions 

1. **Enhanced Loss Function**: Incorporate elements like the UPDRS score and medication information, as well as other data captured by the Verily watch
2. **Missing Data Handling**: Implement masking for real-world adherence patterns
3. **Data Smoothing**: Reduce noise while preserving underlying patterns; investigate imputation alternatives
4. **Validation-Based Training**: Replace convergence-based stopping with validation metrics
5. **Multi-Scale Analysis**: Explore different temporal scales beyond weekly aggregation

## Acknowledgements 
This work was completed as a Bachelor of Science senior thesis in at Yale University. Thanks to Dr. Hemant Tagare for his continuous guidance and supervision, the Yale S&DS department for their academic support, PPMI and Verily Life Sciences for providing the dataset, and my aunt—whose courage while living with PD drove this research. 
