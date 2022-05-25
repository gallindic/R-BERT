This is a forked project of [R-BERT](https://github.com/jmshen1994/R-BERT). It is an unofficial pytorch implementation of R-BERT model described paper [Enriching Pre-trained Language Model with Entity Information for Relation Classification](https://arxiv.org/abs/1905.08284).

## Datasets used
 - SemEval
 - TermFrame (EN/SL)

## Prerequisites

1. Run `pip install -r requirements.txt`

## How to train/eval

All configurations are set in `config.ini`. To train or eval run `CUDA_VISIBLE_DEVICES=0 python r_bert.py --config config.ini`. The evaluation is ran on all the checkpoints in the output folder.

1. On TermFrame (EN/SL)
 - To train set `data_dir=./data/termframe_[eng/slo]`, `task_name=termframe_[eng/slo]`, `output_dir=./output/termframe_[eng/slo]`, `train=True`, `eval=False`, `save_steps=100-200`
 - To eval set `train=False`, `eval=True` and it will evaluate for all checkpoints

2. On SemEval
 - To train set `data_dir=./data/semeval`, `task_name=semeval`, `output_dir=./output/semeval`, `train=True`, `eval=False`, `save_steps=[optional number]`
 - To eval set `train=False`, `eval=True` and it will evaluate for all checkpoints

## Transfer learning

First in the `utils.py` change TERMFRAME_RELATION_LABELS, to use the mapped labels. To use the weights from training on SemEval run with following configuration settings:
```
task_name=termframe_[eng/slo]
output_dir=./output/semeval
data_dir=./data/termframe[eng/slo]
train=True  #Change for evaluation
eval=False  #Change for evaluation
```
Keep in mind that this will create a checkpoint in the semeval folder, which can be moved to a seperate location and that location is used as output for evaluation (otherwise it will run on all the checkpoints in the semeval output folder).