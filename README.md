
# knowledge-graphformer

## What do transformers learn?
Unlike word embeddings which learn the co-occurence of words into one single global vector, transformers learn _Instance specific (kind of Contextual) word vectors_. ie. the vectors vary for the same word based on the sentence it occurs.

Transformers are known to learn something similar to knowledge graphs within their attention matrices.

[Visualizing and Measuring the Geometry of BERT](https://arxiv.org/pdf/1906.02715.pdf) have shown that "just as there are specific syntactic subspaces, there is evidence for
subspaces that represent semantic information"

## knowledge-graphs and transformers

* Understanding a piece of text involves understanding every word within it
* Word embeddings are useful since they provide context for every word within the sentence
* Fundamentally, words / tokens are knowledge about the world
* Do embeddings which give subgraphs of every node (word) enable better understanding of the text?
* Currently, language modelling - learning to predict the next word - learns word respresentations along with language syntax in a way
* This semi supervised method enables us to train with large amounts of data

I try to ask the following questions
* By combining word and language representations, are we complicating the problem?
* Can we have a knowledge graph embedding (of every word) and a language syntax (learnt as weights) separately learnt by the transformer?

#### This variation of the transformer model aims to learn Graph Embeddings + Language syntax in separate embedding subspaces by design

* By learning the KG separately, this gives us a kind of universal language model which can be used for multiple languages with only the syntax model change


` Note: This is a Work in Progress!! `

The base transformer implementation is forked from [transformer-pytorch](https://github.com/tunz/transformer-pytorch)

## Prerequisite

It's using [SpaCy](https://spacy.io/usage/) to tokenize languages for wmt32k
dataset. So, if you want to run `wmt32k` problem which is a de/en translation
dataset, you should download language models first with the following command.

```
$ pip install spacy
$ python -m spacy download en
$ python -m spacy download de
```

## Usage

1. Train a model.
```
$ python train.py --problem wmt32k --output_dir ./output --data_dir ./wmt32k_data
or
$ python train.py --problem lm1b --output_dir ./output --data_dir ./lm1b_data
```

If you want to try `fast_transformer`, give a `model` argument after installing
[tcop-pytorch](https://github.com/tunz/tcop-pytorch).
```
$ python train.py --problem lm1b --output_dir ./output --data_dir ./lm1b_data --model fast_transformer
```


2. You can translate a single sentence with the trained model.
```
$ python decoder.py --translate --data_dir ./wmt32k_data --model_dir ./output/last/models
```
