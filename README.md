# AI-Driven Clinical Decision Support: Enhancing Disease Diagnosis Exploiting Patients Similarity

This repository is the official implementation of [AI-Driven Clinical Decision Support: Enhancing Disease Diagnosis Exploiting Patients Similarity](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9676651). 


## Requirements

To install requirements:

```setup
$ wget https://github.com/facebookresearch/fastText/archive/v0.9.2.zip
$ unzip v0.9.2.zip
$ cd fastText-0.9.2
$ make

$ git clone https://github.com/epfml/sent2vec
$ pip install .

$ pip install --user -U nltk
```

Test data sets are located at sentence-similarity/test_data. The pretrained model BioSentVec_PubMed_MIMICIII-bigram_d700.bin can be placed at sentence-similarity/test_data

## Training

To train the model in the paper, run this command:

```train
./fasttext sent2vec -input inputdata.txt -output model.bin -minCount 8 -dim 700 -epoch 9 -lr 0.2 -wordNgrams 2 -loss ns -neg 10 -thread 20 -t 0.000005 -dropoutK 4 -minCountLabel 20 -bucket 4000000 -maxVocabSize 750000 -numCheckPoints 10
```

To train a new sent2vec model, you first need some large training text file. This file should contain one sentence per line. 

## Evaluation

To evaluate the results using the pretraiined model, run:

```eval
jupyter run Project_244.ipynb
```

This evaluates results on BIOSSES, MayoSRS and UMNRS similarity test data sets using BioSentVec model approach and Levenshtein distance approach.

## Pre-trained Models

We used pretrained models which can be downloaded here:

- [BioSentVec model](https://ftp.ncbi.nlm.nih.gov/pub/lu/Suppl/BioSentVec/BioSentVec_PubMed_MIMICIII-bigram_d700.bin) trained on PubMed+MIMIC-III using  sent2vec to compute the 700-dimensional sentence embeddings. We used the bigram model and set window size to be 20 and negative examples 10. 


## Results

Our model achieves the following performance on :

### [Image Classification on ImageNet](https://paperswithcode.com/sota/image-classification-on-imagenet)

| Model         | BIOSSES  | MayoSSRS |  UMNRS similarity|
| :-------------|---------:| --------:|  ---------------:|
| BioSentVec    |  0.557   |  0.251   |      0.234       |
| Levenshtein   |  0.312   |  0.104   |      0.128       |


## References

- C. Comito, D. Falcone and A. Forestiero, "AI-Driven Clinical Decision Support: Enhancing Disease Diagnosis Exploiting Patients Similarity" in IEEE Access, vol. 10, pp. 6878-6888, 2022, doi: 10.1109/ACCESS.2022.3142100
- Chen Q, Peng Y, Lu Z. BioSentVec: creating sentence embeddings for biomedical texts. 2018. arXiv:1810.09302.
- Zhang Y, Chen Q, Yang Z, Lin H, Lu Z. BioWordVec, improving biomedical word embeddings with subword information and MeSH. Scientific Data. 2019.

