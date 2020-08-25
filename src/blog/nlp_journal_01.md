---
title: Machine Learning - NLP Journal 
date: 2020-08-03 00:00:00
excerpt: PEGASUS [Pre-training with Extracted Gap-sentences for Abstractive Summarization] Research Paper by Jingqing Zhang, Yao Zhao, Mohammad Saleh, Peter J. Liu
type: post
blog: true
---

Text summarization generates succinct summaries with precision and accuracy from input text. There are two main approaches to text summarization in Natural Language Process (NLP), the extraction based summarization and the abstraction based summarization.

Extraction based summarization uses key phrases from source input and combine them to create a summary while the abstraction based summarization is a more sophiscated method by paraphrasing and generating new sentences which are not present in the input source.

In this paper, PEGASUS - a sequence to sequence model with gap sentences generation as a pre-training objective tailored is proposed for abstractive text summarization. 

## What is sequence to sequence model
Sequence to sequence model  maps input text to output text. Seq2seq model is based on the encoder-decoder architecture to create a sequence output for a sequence input. Unlike the standard network which only maps fixed length inputs to outputs, both encoder and decoder use recurrent neural networks (RNNs) to tackle sequence inputs of different length.
 ![ seq2seq's Photo ](/seq2seq.svg)

The layers in the encoder and the decoder are illustrated in Fig. 9.7.2.

 ![seq2seq-details's Photo ](/seq2seq-details.svg)

 Reference: [Dive Into Deep Learning](https://d2l.ai/chapter_recurrent-modern/seq2seq.html)

 ## Summarizing paper's contribution
 New self supervised pre-training objective for abstractive summarization with Gap Sentences Generation (GSG), and study strategies for selecting those sentences
 ### Gap Sentences Generation (GSG)
 Hypothesize suggests using a pre-training objective similar to achieving the goal of downstream task leads to better performance. 

 * Downstream task refers to task further down the pipeline, credits to Reddit community, an explaination to this can be: Imagine you have a pre-trained word embedding model trained on next-word prediction. You can use those vectors on a down-stream task (say, text classification) by using the word vectors (or rather, pooled word vectors = document vectors) as input to a final ML model (usually a linear SVM or neural network since this is usually a high dimensional space) to do a downstream task like textual classification.

Sentiment analysis, some kinds of summarization, etc are also downstream tasks. It's "downstream" if your pretrained model wasn't directly trained on that task but you're using it with in combination with a final classifier.

Naive approach in pre-training as an extractive summarizer trains a model to copy sentences which is not ideal for abstractive summarization. Instead, selectiving and masking whole sentences from input text and concatenate the gap sentences into a pseudo-summary is adopted. The corresponding position of each selected gap sentences is subsituted with a mask token represented in `[MASK]` to inform the model. Gap sentences ratio (GSR), also known as the mask rate, is the number of selected gap sentences to the total number of sentences in input text.

For further enhancement, sentences that deem to be more important to the input source is being selected. Three primary strategies for selecting m gap sentences from a document with n sentences are: random - m sentences are uniformly selected at random , lead - first m sentences are selected or principal selection - select top-m scored sentences according to importance. 

Sentences are scored independently (Ind) and the top m sentences are selected. Selecting sentences sequentially (Seq) by greedily maximising the ROUGE1-F1 between selected sentences and remaining sentences is also being considered. 

## ROUGE Scoring
ROUGE coins for Recall-Oriented Understudy for Gisting Evaluation. It is a set of metrics for summarization evaluation and machine translation by comparing an automaticall generated summary or translated document from machine with a set of reference summaries which are usually done by human.

### Recall in ROUGE
Recall in ROUGE measures how much of the reference summary is the system summary capturing. Considering individual words, Recall in ROUGE can be calculated as number of overlapping words divided by total words in reference summary.

 ![ ROUGE's Photo ](/ROUGE.svg)

In this case, only half of the words in human produced summary is captured by machine produced summary. While a machine produced summary can improve recall scoring with a longer summary, thus capturing all words from the human produced summary, summary with unnecessary words are undesirable. As such, precison scoring in ROUGE is needed to measure how many of the machine produced summary is relevant or needed. With a score of only 0.333, it shows that machine produced summary contains many unnecessay words. Measure of precision is important to generate concise summary. Computation of both Recall and Precision is reported as the F-measure.

### Variants of ROUGE - ROUGE-N, ROUGE-S, ROUGE-L
Quoting from text-analytics101:
> ROUGE-N, ROUGE-S and ROUGE-L can be thought of as the granularity of texts being compared between the system summaries and reference summaries

Example: ROUGE-1 refers to the overlap of unigrams between system and reference summary. ROUGE-2 refers to the overlap of bigrams between system and reference summary.

#### What is n-gram?
Simply put, one word is one gram, so n words are n grams.

#### Different ROUGE Measures from [text-analytics101](http://text-analytics101.rxnlp.com/2017/01/how-rouge-works-for-evaluation-of.html)
- ROUGE-N: measures unigram, bigram, trigram and higher order n-gram overlap
- ROUGE-L:  measures longest matching sequence of words using LCS. An advantage of using LCS is that it does not require consecutive matches but in-sequence matches that reflect sentence level word order. Since it automatically includes longest in-sequence common n-grams, you don't need a predefined n-gram length.
- ROUGE-S: Is any pair of word in a sentence in order, allowing for arbitrary gaps. This can also be called skip-gram coocurrence. 

### Masked Language Model (MLM)
MLM is applied to train the Transformer as the only pre-training objective or together with GSG. However, the paper shows that MLM does not improve downstream tasks at large number of pre-training steps.

### Datasets 
- [XSum](http://bollin.inf.ed.ac.uk/public/direct/XSUM-EMNLP18-Summary-Data-Original.tar.gz)
- [CNN/DailyMail process data by jafferwilson](https://drive.google.com/file/d/0BzQ6rtO2VN95a0c3TlZCWkl3aU0/view?usp=sharing)
- [NEWSROOM](http://lil.nlp.cornell.edu/newsroom/download/index.html)
- [Multi-News](https://drive.google.com/open?id=1jwBzXBVv8sfnFrlzPnSUBHEEAbpIUnFq)
- [Gigaword](https://github.com/harvardnlp/sent-summary)
- [arXiv](https://drive.google.com/file/d/1b3rmCSIoh6VhD4HKWjI4HOW-cSwcwbeC/view)
- [PubMed](https://drive.google.com/uc?id=1lvsqvsFi3W-pE1SqNZI0s8NR9rC1tsja&export=download)
- [BIGPATENT](https://drive.google.com/uc?export=download&id=1J3mucMFTWrgAYa3LuBZoLRR3CzzYD3fa)
- [WikiHow](https://ucsb.app.box.com/s/ap23l8gafpezf4tq3wapr6u8241zz358)
- [Reddit TIFU](https://drive.google.com/uc?id=1ffWfITKFMJeqjT8loC8aiCLRNJpc_XnF&export=download)
- [AESLC](https://github.com/ryanzhumich/AESLC)
- [BillSum](https://drive.google.com/uc?id=1SkwK-PfcHzznKUHy2S3jfdITR4D5MD5u&export=download)

### Experiments
Sinusoidal positional encoding and greedy-decoding are used. For optimisation,Adafactor with square root learning rate and dropout rate = 0.1 is used for both pre-training and finetuning. Beam search with a length-penalty is used for large model.

### Results
Pre-training models transfer more effectivelt to downstream tasks when their domains are more similar. Indi-Orig GSG has the best performance followed by Seq-Uniq amongst six GSG approaches (Lead, Random, Ind-Orig, Ind-Uniq, Seq-Orig, Seq-Uniq). The improvement from a Transformer model without pre-training to PEGASUS(large) was more significant on smaller datasets. Small text summariation datasets gain the most from pre-training.

#### Effect of vocabulary
Byte-pair encoding algorithm(BPE) and SentencePiece Unigram algorithm (Unigram) tokenization methods are used. Both BPE and Unigram are comparable on news datasets while Unigram has better performance on non-news datasets.

#### Limitation of ROUGE
ROUGE overpenalizes abstractive approaches compared to extractive summaries. Summaries that are mostly paraphrased would less likely to score well since there will be lesser overlapping words. Also, ROUGE neglects linguistic quality of the summaries.