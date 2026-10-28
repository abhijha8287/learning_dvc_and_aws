# DVC Pipeline with S3 (Spam Classifier)

A five-stage spam-detection pipeline run with DVC, with parameters, experiment tracking and an S3 remote.

## Why this exists
Practice with DVC pipelines: reproducible stages, parameter changes, experiments with DVCLive, and remote storage on AWS S3.

## What it does
- `data_ingestion`: downloads the SMS spam dataset and splits it (test size from `params.yaml`)
- `data_preprocessing`: cleans and normalises the text
- `feature_engineering`: TF-IDF features (`max_features` from `params.yaml`)
- `model_building`: random forest (`n_estimators`, `random_state` from `params.yaml`)
- `model_evaluation`: writes metrics to `reports/metrics.json` and logs them with DVCLive

## Project structure
```
learning_dvc_and_aws/
├── src/              One script per pipeline stage
├── experiments/      Exploration notebook and raw data
├── dvclive/          Tracked params, metrics, plots
├── reports/          Final metrics
├── dvc.yaml          Pipeline stages
├── params.yaml       Tunable parameters
├── projectflow.txt   Step-by-step build notes
└── LICENSE           MIT licence
```

## Getting started
Requirements: Python 3.10+, DVC; AWS credentials for the S3 remote.
```bash
git clone https://github.com/abhijha8287/learning_dvc_and_aws.git
cd learning_dvc_and_aws
pip install dvc dvclive "dvc[s3]" pandas scikit-learn nltk
dvc repro                  # run all stages
dvc exp run                # run an experiment after editing params.yaml
dvc exp show               # compare experiments
dvc push                   # upload data and models to S3
```

## Configuration
The DVC remote is `s3://dvc-s3-learning`. Set `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`, or run `aws configure`, before `dvc push`.

## Tech stack
Python, scikit-learn, NLTK, DVC, DVCLive, AWS S3

## Notes
MIT licensed.
