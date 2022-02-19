# Block-wise Word Embedding Compression Revisited: Better Weighting and Structuring

### Overview
This repository contains the official implementation for the paper, ["Block-wise Word Embedding Compression Revisited: Better Weighting and Structuring", Findings of EMNLP 2021](https://aclanthology.org/2021.findings-emnlp.372).
It contains all the implementations for the paper, and we are working on 100% reproduction with yaml-based configuration for convenience.

### Requirements
* python3, torch, scipy, numpy for discblock. For each task, you need to install required packages.
torch == 1.7.1
torchtext == 0.8.1
yaml
scipy

### Getting Started
This repository provides various tasks for experiments.
Let us show how to apply our method with language modeling.

#### Step 1: Train a base model
```
$ cd experiments/lm/medium
$ python ../../../run_lm.py --config base.yaml
```

#### Step 2: Compute the TF-IDF based Word Importance Score
```
$ cd tasks/lm
$ python get_tfidf.py --data ptb --model tfidf
```
The example dataset is PennTree Bank and the TF-IDF based scoring scheme is used.

#### Step 3: Compute Differentiable Word importance Score
```
$ cd experiment/lm/diff
$ python ../../../run_lm.py --config config.yaml
```
The path to the base model and all hyper-parameters are already set in `config.yaml`.

#### Step 4: Block-wise Embedding Compression and Fine-tuning
```
$ cd experiment/lm/diff_score
$ python ../../../run_lm.py --config config.yaml
```
In the same way, all the hyper-parameters are already set in `config.yaml`.

### Compression Performance

#### After Retraining (about 20x compression ratio) 

| Datasets     |      Original Score      |	SVD						|	DisckBlock-F	|  DiscBlock-T |	DiscBlock-D	|
|--------------|:------------------------:|--------------:|--------------:|-------------:|-------------:|
| 	PTB	 	     |						80.8				  |	96.0					|	92.9					| 92.0 				 |		88.7			|
| WikiText2    |   					93.3				  |	115.0					|	107.8					| 104.3 			 |		102.7			|
| WikiText103  | 						61.0				  |	83.2					|	82.5					| 72.4 				 |		67.6			|

### Tasks

#### Language Modeling
Our implementation for language modeling is based on https://github.com/pytorch/examples/tree/master/word_language_model.
For handling this task, use `run_lm.py` and see `tasks/lm`.

#### Neural Machine Translation
Our implementation for NMT is based on https://github.com/joeynmt/joeynmt.
For handling this task, use `run_joeynmt.py` and see `tasks/joeynmt`.
`tasks/joeynmt/third_party` contains a variation of joeynmt.

#### SNLI
Our implementation for NMT is based on https://github.com/imran3180/pytorch-nli.
For handling this task, use `run_snli.py` and see `tasks/snli`.
`tasks/snli/third_party` contains a variation of pytorch-nli.

#### SST-5
Our implementation for NMT is based on https://github.com/Doragd/Text-Classification-PyTorch.
For handling this task, use `run_sst.py` and see `tasks/sst`.
`tasks/sst/third_party` contains a variation of the original repository..

#### SQuAD
Our implementation for SQuAD is based on https://github.com/HazyResearch/smallfry including the implementation for SmallFry.
For handling this task, use `run_drqa.py` and see `tasks/drqa`.
`tasks/drqa/third_party` contains a variation of DrQA.

#### Knowledge Embedding
Our implementation for KE is based on https://github.com/thunlp/OpenKE.
For handling this task, use `run_ke.py` and see `tasks/ke`.
`tasks/ke/third_party` contains a variation of OpenKE.

### Acknowledgement
This work was supported by Institute of Information & communications Technology Planning & Evaluation (IITP) grant funded by the Korea government(MSIT) (No. 2021-0-00907, Development of Adaptive and Lightweight Edge-Collaborative Analysis Technology for Enabling Proactively Immediate Response and Rapid Learning).
