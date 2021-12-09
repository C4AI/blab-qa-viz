# Interpretability of Attention Mechanisms  in a Portuguese-Based Question Answering System about the Blue Amazon
Repository for the ENIAC'21 paper "Interpretability of Attention Mechanisms  in a Portuguese-Based Question Answering System about the Blue Amazon"

The full paper can be found: https://sol.sbc.org.br/index.php/eniac/article/view/18302


## Abstract

The Brazilian Exclusive Economic Zone, or the "Blue Amazon", with its extensive maritime area, is the primary means of transport for the country's foreign trade and is important due to its oil reserves, gas and other mineral resources, in addition to the significant influence on the Brazilian climate. We have manually built a question answering (QA) dataset based on crawled articles and have applied an off-the-shelf QA system based on a fine-tuned BERTimbau Model, achieving an F1-score of 47.0. More importantly, we explored how the proper visualization of attention weights can support helpful interpretations of the system's answers, which is critical in real environments.

## Blue Amazon QA Database

File: Blue_Amazon_QA_dataset.csv

This dataset is composed of 400 questions created by specialists about the blue amazon from wikipedia articles and the book "Coastal fisheries of Latin America and the Caribbean".

For the creation of the questions, a bot was built which is found on github: 

The file is Blue_Amazon_QA_dataset.csv and can be read using the pandas library: 

```
import pandas as pd

df = pd.read_csv('Blue_Amazon_QA_dataset.csv')
```

The columns of the dataset are:
* Question_ID: ID of the question
* Source: File that origininated the question. It is important to note that the name is the wikipedia article or the part of the book relative to the Brazilian Coast
* book/wikipedia: this column just indicate if the origin (wikipedia article or book)
* Passage: the passage/paragraph that originated the question
* Question: the question
* Answer: the answer
* Passagem: translation, via google translator, of the passage to Portuguese 
* Questão: translation, via google translator, of the question to Portuguese 
* Resposta: translation, via google translator, of the answer to Portuguese 


## Portuguese BERT SQuAD model performance on the Blue Amazon QA Dataset

File: BERT_Performance_Evaluation-Blue_Amazon_QA.ipynb

As described better in the paper, a code was created that verified the performance of the bert-base-cased-squad-v1.1-portuguese model (which can be found at: https://huggingface.co/pierreguillou/bert-base -cased-squad-v1.1-english) in the Blue Amazon QA dataset. 

As with the SQuAD dataset (https://rajpurkar.github.io/SQuAD-explorer/), the questions are accompanied by a passage from which the answer is derived. In this case, translations into Portuguese were used and the results were: 

F1-Score  | EM (Exact Match)  | Rouge-L
--------- | ----------------  | -----------
53.1      | 22.3              | 53.4


Disclaimer: the results presented here differ from what was presented in the paper because a manual analysis of the questions and answers was performed, which corrected errors. This improved the overal quality of the dataset, and ended up increasing the performance of the model. 

## Results of the Portuguese BERT SQuAD model performance on the Blue Amazon QA Dataset

File: Results/Blue_Amazon_QA-SQuAD_Results.csv

This this file is composed of the results of the BERT_Performance_Evaluation-Blue_Amazon_QA.ipynb, and has the true and generated answer for comparison.

The file can be read using the pandas library: 

```
import pandas as pd

df = pd.read_csv('Results/Blue_Amazon_QA-SQuAD_Results.csv', index_col = 0)
```

The columns of the File are:
* question: Question in Portuguese
* passages: Passage in Portuguese
* true_answers: Annotated answer of the dataset
* gen_answers: generated answer of the model bert-base-cased-squad-v1.1-portuguese
* f1-score: F1-Score metric of true_answer with gen_answer
* rouge_L: Rouge-L metric of true_answer with gen_answer
* EM: Exact Match metric of true_answer with gen_answer


## Cite this work

```
@inproceedings{eniac,
 author = {Stefano Spindola and Marcos José and André Oliveira and Flávio Cação and Fábio Cozman},
 title = {Interpretability of Attention Mechanisms in a Portuguese-Based Question Answering System about the Blue Amazon},
 booktitle = {Anais do XVIII Encontro Nacional de Inteligência Artificial e Computacional},
 location = {Evento Online},
 year = {2021},
 keywords = {},
 issn = {0000-0000},
 pages = {775--786},
 publisher = {SBC},
 address = {Porto Alegre, RS, Brasil},
 url = {https://sol.sbc.org.br/index.php/eniac/article/view/18302}
}
```