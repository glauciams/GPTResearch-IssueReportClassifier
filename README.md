<!-- ![nlbse 2024](nlbse2024.png) -->

# NLBSE'24 Tool Competition on Issue Report Classification

## Introduction

The issue report classification competition consists of building and testing a set of multi-class classification models 
to classify issue reports as belonging to one category representing the type of information they convey.

We provide a dataset encompassing 3 thousand labeled issue reports 
(as bugs, enhancements, and questions) 
extracted from 5 real open-source projects. 
You are invited to leverage this dataset for evaluating your classification approaches and compare the achieved results against proposed baseline approaches based on Sentence-Transformers.

You must train, tune and evaluate your multi-class classification models using the provided training and test sets.

> Please refer to our [tool competition page](https://nlbse2024.github.io/tools/) to read more about the tool competition and learn how to participate.

## Citing related work

Since you will be using our dataset (and possibly one of our notebooks) as well as the original work behind the dataset, please cite the following references in your paper:

```bibtex
@inproceedings{nlbse2024,
  author={Kallis, Rafael and Colavito, Giuseppe and Al-Kaswan, Ali and Pascarella, Luca and Chaparro, Oscar and Rani, Pooja},
  title={The NLBSE'24 Tool Competition},
  booktitle={Proceedings of The 3rd International Workshop on Natural Language-based Software Engineering (NLBSE'24)},
  year={2024}
}
```

```bibtex
@article{kallis2020tickettagger,
  author={Kallis, Rafael and Di Sorbo, Andrea and Canfora, Gerardo and Panichella, Sebastiano},
  title={Predicting issue types on GitHub},
  journal={Science of Computer Programming},
  volume={205},
  pages={102598},
  year={2021},
  issn={0167-6423},
  doi={https://doi.org/10.1016/j.scico.2020.102598},
  url={https://www.sciencedirect.com/science/article/pii/S0167642320302069}
}
```

```bibtex
@inproceedings{kallis2019tickettagger,
  author    = {Kallis, Rafael and Di Sorbo, Andrea and Canfora, Gerardo and Panichella, Sebastiano},
  title     = {Ticket Tagger: Machine Learning Driven Issue Classification},
  booktitle = {2019 {IEEE} International Conference on Software Maintenance and Evolution,
               {ICSME} 2019, Cleveland, OH, USA, September 29 - October 4, 2019},
  pages     = {406--409},
  publisher = { {IEEE} },
  year      = {2019},
  doi       = {10.1109/ICSME.2019.00070},
}
```

## Dataset

A dataset of 3 thousand publicly-available issue reports is extracted.

Each issue report contains the following information:
- Repository
- Label
- Title
- Body

Each issue is labeled with one class that indicates the issue type, namely, `bug`, `feature`, and `question`.

Issues with multiple labels are excluded from the dataset.

The dataset is then split into a training set (50%) and a test set (50%).

The process of extracting the dataset is described in the [dataset notebook](1-Dataset.ipynb).

> The dataset has already been extracted to avoid costs on your end, please keep reading to find hyperlinks to both the training and test set.

## Training

You are provided a [training set](https://raw.githubusercontent.com/nlbse2024/issue-report-classification/main/data/issues_train.csv?token=GHSAT0AAAAAACG4EVQDBT5ISO7BHQ5PV63QZI63Z6Q) encompassing 1.5 thousand labeled issue reports extracted from 5 real open source projects. The training-set is balanced, i.e., it contains the same number of issues for each class.

Participants must train a multi-class classifier for each of the 5 projects, i.e., we expect 5 classifiers per model submission.

Participants are free to select and transform variables from the training set as they please. Pretrained models are permitted but can only be finetuned on the given training set. Any inputs or features used to create or finetune the classifier, must be derived from the provided training set. Participants may preprocess, sample, apply over/under-sampling, select a subset of the attributes, perform feature-engineering, filter records, split the training set into a model-finetuning validation set, etc. Please contact us if you have any question about this.

## Evaluation

Submissions are evaluated based on their class-detection performance over the provided [test set](https://raw.githubusercontent.com/nlbse2024/issue-report-classification/main/data/issues_test.csv?token=GHSAT0AAAAAACG4EVQDKGFUQA2CR27PPS2SZI633MA). 
The classifier should assign one label to an issue. Just like the training set, the test set is balanced.

Participants must evaluate their project classifiers on the test set of the respective project and report the results in their submission.

**Important:** you may apply any preprocessing or feature engineering on this dataset except sampling, rebalancing, undersampling or oversampling techniques.

Repository classification performance is measured using the F1 score over all the three classes (averaged). Cross-repository performance is measured as the arithmetic mean of the five repository F1 scores.

A submission (i.e., paper) in the tool competition must provide, for each of the 5 repositories and cross-repo:
- Precision, for each class and cross-class average
- Recall, for each class and cross-class average
- F1 score, for each class and cross-class average

Cross-class aggregation can be done using both the macro and micro averaging method, the result will be the same since the dataset is balanced.

Cross-repo aggregation is done using the arithmetic mean.

Please note that whilst all of the above measures must be provided for acceptance, the submissions will **only** be ranked by their cross-repo F1 score.

> You can use the table from the baseline below as a template for your evaluation.

## Baselines

Participants are encouraged, but not required, to use the baseline as a template for their submission. Each template downloads the dataset, performs basic preprocessing, trains a set of classifiers and evaluates them on the test set.

### [SetFit](2-Template-SetFit.ipynb)

| Repository            | Label         | Precision | Recall | F1         |
| --------------------- | ------------- | --------- | ------ | ---------- |
| facebook/react        | bug           | 0.0000    | 0.0000 | 0.0000     |
| facebook/react        | feature       | 0.0000    | 0.0000 | 0.0000     |
| facebook/react        | question      | 0.0000    | 0.0000 | 0.0000     |
| facebook/react        | average       | 0.0000    | 0.0000 | 0.0000     |
| | | | | |
| tensorflow/tensorflow | bug           | 0.0000    | 0.0000 | 0.0000     |
| tensorflow/tensorflow | feature       | 0.0000    | 0.0000 | 0.0000     |
| tensorflow/tensorflow | question      | 0.0000    | 0.0000 | 0.0000     |
| tensorflow/tensorflow | average       | 0.0000    | 0.0000 | 0.0000     |
| | | | | |
| microsoft/vscode      | bug           | 0.0000    | 0.0000 | 0.0000     |
| microsoft/vscode      | feature       | 0.0000    | 0.0000 | 0.0000     |
| microsoft/vscode      | question      | 0.0000    | 0.0000 | 0.0000     |
| microsoft/vscode      | average       | 0.0000    | 0.0000 | 0.0000     |
| | | | | |
| bitcoin/bitcoin       | bug           | 0.0000    | 0.0000 | 0.0000     |
| bitcoin/bitcoin       | feature       | 0.0000    | 0.0000 | 0.0000     |
| bitcoin/bitcoin       | question      | 0.0000    | 0.0000 | 0.0000     |
| bitcoin/bitcoin       | average       | 0.0000    | 0.0000 | 0.0000     |
| | | | | |
| opencv/opencv         | bug           | 0.0000    | 0.0000 | 0.0000     |
| opencv/opencv         | feature       | 0.0000    | 0.0000 | 0.0000     |
| opencv/opencv         | question      | 0.0000    | 0.0000 | 0.0000     |
| opencv/opencv         | average       | 0.0000    | 0.0000 | 0.0000     |
| | | | | |
| average               | bug           | 0.0000    | 0.0000 | 0.0000     |
| average               | feature       | 0.0000    | 0.0000 | 0.0000     |
| average               | question      | 0.0000    | 0.0000 | 0.0000     |
| average               | average       | 0.0000    | 0.0000 | **0.0000** |
