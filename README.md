# AgnosticFaceSynthesisDetection

<img src="https://github.com/kopepod/AgnosticFaceSynthesisDetection/blob/main/FIGS/Pipeline.png" width="1200" height="200" />

[![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1Ifrd_-ogXG6KM8Lb3w72GXclZjXB9dvz)
[![arXiv](https://img.shields.io/badge/arXiv-1234.56789-b31b1b.svg)](https://arxiv.org/abs/2401.04241)

This is the implementation of the paper entitled _Data-Agnostic Face Image Synthesis Detection Using Bayesian CNNs_ this repository is divided as follows:

1. Create Environment
2. Dataset
3. Train Models
4. Test Models

## Create Environment

To create the environment you have to install [anaconda](https://www.anaconda.com/download) and run the following command:
```bash
conda env create -f environment.yml
```
You should be able to run this command:
```bash
conda run -n CBN python --version
```
## Dataset

It is necessary to download the [FFHQ](https://github.com/NVlabs/ffhq-dataset) dataset from the original authors. Create the following structure with the Real and Synthetic Images:

```bash
tree
.
└── FFHQ
    ├── Fake
    │   └── 0
    │       ├── seed0000.png
    │       ├── seed0001.png
    │       └── seed0002.png
    └── Real
        └── 0
            ├── 00000.png
            ├── 00001.png
            └── 00002.png
```
Where the Real is the folder comprises the FFHQ samples and the Fake the ones generated from the synthesizer, respectively.

## Train Models

We can pass specific parameters to train the models. Running the following command you will observe what the parameters control.

```bash
python Main.py TrainModel  --help 

usage: Fake Synthesis Detection via Bayesian CNN TrainModel [-h] [--Epochs EPOCHS] [--LR LR] [--BS BS] [--GPU GPU] [--DatasetPath DATASETPATH] [--ModelPath MODELPATH] [--n_samples N_SAMPLES] [--Split SPLIT]

This code trains a model from unlabeled data

options:
  -h, --help            show this help message and exit
  --Epochs EPOCHS       Number of epochs to train the Model
  --LR LR               Learning Rate
  --BS BS               Batch Size
  --GPU GPU             GPU id device
  --DatasetPath DATASETPATH
                        Training samples path
  --ModelPath MODELPATH
                        Path to save model
  --n_samples N_SAMPLES
                        Number of samples to predict from the Bayesian Model
  --Split SPLIT         Partition size to train/test the model

```

There are defaults, thus the model is trained as

```bash
python Main.py TrainModel --Epochs 5 --BS 128
```
The process generates a JSON file resuming the training.

## Test Models

Similarly to the previous script, query samples can be tested as follows:

```bash
python Main.py TestModel --GPU 0 --DatasetPath <> --OutFile FakeINSGEN.json --ModelPath ./MODELS/<>/
```




