# TerminologyM2TAL-DG
Terminology project - M2 TAL - 2020/2021

This repository implements two rule-based identification systems that tag a document with the IOB tagset for multiword terms.

### The IOB tagset for multiword terms :

- B : Beginning of multiword term
- I : Inside a multiword term (not at the beginning)
- O : outside a term

## Run

To run this project, you just have to open the TerminologyProject.ipynb in jupyter notebook and run all the cells.
It will follow the order and instructions bellow.

## Rule-based identification system 1 :

The first rule-based identification system is created from scratch with SpaCy. The idea of the process is to tokenzie a (or many) desired document and loop on the word to tag it one by one with the use of heuristics to enable one insert joker word. This system did not manage the generation of syntactic variants.

The output txt file is stored in the /Corpus/ directory.

## Rule-based identification system 2 : 

The second rule-based identification system is created with the flair framework for state-of-the-art NLP.

Check https://github.com/flairNLP/flair for more informations about this framework.

First, we load our Training Data which come from our own sequence labeling Dataset (created with the first rule-based identification system). The column format is constitute by two column, the first column is the word itself and the second is the IOB-annotated tags for Terms. Empty line separates sentences. To read such a dataset, define the column structure as a dictionary and instantiate a "ColumnCorpus".

This gives you a Corpus object that contains the train, dev and test splits, each has a list of Sentence.

After that, we have to train our new Sequence Labeling Model.  We get the corpus, we initatiate that we want to predict the IOB tag, we make a tag dictionary from the corpus, we initialize the stacked embedding with GloVe and finally we initialize the sequence tagger, the trainer and we start the training. If you don't have cuda on your device, you must remove the "embeddings_storage_mode='gpu'" in the "train()" method.

Finally, once the model is trained you can load it to predict the class of new sentences.

## Next 

For now, our corpus is only 30 articles. You can increase the number by adding .txt files in the /Articles/txt/ directory.

## Acknowledgement 

We have already extract automatically the terms from our corpus with TermSuite. You must provide a .tsv file with the terms you want to annotate for your corpus or you can use the one already in our repository. For more informations : http://termsuite.github.io/ 

## Created by

Axel Didier - M2 TAL  /  Pierre Goncalves - M2 TAL
