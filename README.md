# End to End ML Pipeline using DVC and AWS S3

---

## Overview

This project demonstrates a robust, modular, and reproducible end-to-end machine learning pipeline for text classification (spam detection), leveraging DVC for data and experiment versioning, and AWS S3 for scalable remote storage. The pipeline is designed for extensibility, transparency, and ease of collaboration.

---

## Project Structure

- **src/**: Contains modular Python scripts for each pipeline stage:
  - `data_ingestion.py`: Downloads and splits raw data.
  - `data_preprocessing.py`: Cleans, encodes, and normalizes text data.
  - `feature_engineering.py`: Extracts features using TF-IDF vectorization.
  - `model_building.py`: Trains a RandomForest model.
  - `model_evaluation.py`: Evaluates the model and logs metrics.
- **experiments/**: Contains Jupyter notebooks and datasets for experimentation.
- **logs/**: Stores logs for each pipeline stage for traceability.
- **dvc.yaml**: Defines the DVC pipeline stages and their dependencies.
- **params.yaml**: Centralized configuration for pipeline parameters.
- **dvclive/**: Stores experiment metrics and plots for tracking.
- **.dvc/config**: Configures DVC to use AWS S3 as the remote storage backend.

---

## Pipeline Stages

1. **Data Ingestion**
   - Downloads the dataset and splits it into train/test sets.
   - Parameters (in `params.yaml`): test size.
   - Output: `data/raw/`

2. **Data Preprocessing**
   - Cleans text, removes duplicates, encodes labels, and normalizes.
   - Output: `data/interim/`

3. **Feature Engineering**
   - Applies TF-IDF vectorization to text data.
   - Parameter: max_features.
   - Output: `data/processed/`

4. **Model Building**
   - Trains a RandomForestClassifier.
   - Parameters: n_estimators, random_state.
   - Output: `models/model.pkl`

5. **Model Evaluation**
   - Evaluates the model using accuracy, precision, recall, and AUC.
   - Logs metrics with dvclive and saves to `reports/metrics.json`.

---

## Data & Experiment Versioning

- **DVC** is used to:
  - Track data, models, and metrics.
  - Define and reproduce pipeline stages.
  - Version control large files and datasets.
- **AWS S3** is configured as the DVC remote (`s3://subhdvc`), enabling scalable, cloud-based storage and collaboration.

---

## Tech Stack

- **Programming Language:** Python 3.x
- **ML Libraries:** scikit-learn, pandas, numpy, nltk
- **Feature Extraction:** TfidfVectorizer
- **Model:** RandomForestClassifier
- **Experiment Tracking:** dvclive
- **Pipeline & Data Versioning:** DVC
- **Remote Storage:** AWS S3
- **Logging:** Python logging module
- **Jupyter Notebook:** For experimentation and EDA

---

## How to Run

1. **Install dependencies**  
   *(You may need to create a `requirements.txt` if not present. Typical dependencies: scikit-learn, pandas, numpy, nltk, dvc[s3], dvclive, pyyaml, etc.)*

2. **Configure AWS S3 credentials**  
   Ensure your AWS credentials are set up for DVC to access S3.

3. **Reproduce the pipeline**
   ```bash
   dvc repro
   ```

4. **Track experiments and metrics**
   - Metrics and plots are available in `dvclive/` and `reports/metrics.json`.

5. **Push/pull data and models**
   ```bash
   dvc push   # Uploads data/models to S3
   dvc pull   # Downloads data/models from S3
   ```

---

## Customization

- Modify `params.yaml` to tune hyperparameters and pipeline settings.
- Add new stages or scripts in `src/` as needed.
- Use DVC to add new data or models for versioning.

---

## Best Practices

- All pipeline steps are modular and logged for traceability.
- Data, models, and metrics are versioned for reproducibility.
- Remote storage (S3) enables team collaboration and scalability.
- Experiment tracking with dvclive for ML workflow transparency.

---

## License

This project is licensed under the GPL-3.0 License. 