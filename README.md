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

First, we load our Training Data which come from our own Sequence Labeling Dataset (created with the first rule-based identification system). The column format is constituted by two columns. The first column is the word itself, the second is the IOB-annotated tags for Terms and an empty line separates sentences. To read such a dataset, we define the column structure as a dictionary and instantiate a "ColumnCorpus".

This gives you a Corpus object that contains the train, dev and test splits, each has a list of Sentence.

After that, we have to train our new Sequence Labeling Model. By order, we get the corpus, we initiate that we want to predict the IOB tag, we make a tag dictionary from the corpus, we initialize the stacked embedding with GloVe and finally we initialize the sequence tagger, the trainer and we start the training. If you don't have cuda on your device, you must remove the "embeddings_storage_mode='gpu'" in the "train()" method.

Finally, once the model is trained you can load it to predict the class of new sentences.

## The repository folder :

/Articles/txt/ : initial textual articles data.
/Corpus/ : The train, test and dev txt file annotated with IOB tagset for specific game terms.
(/resources/taggers/example-pos/ : result of the last launch of the TerminologyProject.ipynb with training part, loss report, test comparaison and the identification system model ready to use with flair.) 
/sequencetag_result/ : save result of the training part with f1-score, loss report and test comparaison between the two rule-based identification system.
/TermsTSV/ : tsv output file from TermSuite with the filtered Terms of our specific domain.
MOBA-en-lexicon : list of terms filtered, on our specific domain.
TerminologyProject.ipynb : python script with all the functions used.

## Next 

For now, our corpus is only 30 articles. You can increase the number by adding .txt files in the /Articles/txt/ directory.

## Acknowledgement 

We have already extract automatically the terms from our corpus with TermSuite. You must provide a .tsv file with the terms you want to annotate for your corpus or you can use the one already in our repository. For more informations : http://termsuite.github.io/ 

## Created by

Axel Didier - M2 TAL  /  Pierre Goncalves - M2 TAL
https://github.com/Kroxyl/TerminologyM2TAL-DG/

