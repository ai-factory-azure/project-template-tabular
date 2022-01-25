# Instructions

This is an example demonstrating how to do experimentation during model development.

Use case:
* Tabular-based model training (input to model is tabular data, e.g., parquet or csv)
* Model is then used for batch scoring (input to batch scoring is also tabular data, e.g., parquet or csv)

## Run training locally (without AzureML)

```console
conda env create -f src/environment.yml
conda activate tabular-example
python src/train.py --data_path data/
```

## Run training on AzureML

This will automatically upload and cache the data from `data/` to AzureML:

```console
az configure --defaults group=ai-factory workspace=ai-factory
az ml job create -f azureml/train-azure.yml --stream
```

### Run training on AzureML using Dataset feature

```console
az configure --defaults group=ai-factory workspace=ai-factory
az ml data create --file azureml/dataset.yml # Create dataset in AzureML
az ml job create -f azureml/train-azure-dataset.yml --stream
```

## Run training locally on your own machine (using AzureML)

```console
az configure --defaults group=ai-factory workspace=ai-factory
az ml job create -f azureml/train-azure.yml --set compute.target=local --stream
```

## Run batch scoring locally for testing

```console
python src/batch.py
```