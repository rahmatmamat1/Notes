---
title: Introduction to Large Language Models
tags: 
Created: 2023-10-15T22:38
Updated: 2023-10-15T22:51
---
## What are Large Language Models?

**Large Language Models** are the next advancement in the AI era. With the release of ChatGPT, **Generative AI** has been the most trending topic in the technology world. Large Language Models (LLMs) are part of Generative AI that imitates human intelligence, mainly language and speech. LLMs are known for their capability to generate text-based content. Some other use cases of Large Language Models are Text Summarization, Question and Answering bot, Text completion, Grammar correction, Code Generation, Language Translation and so on.  
  
A simple purpose of a Language model is to serve a purpose to communicate and generate new concepts. The term large here indicates the corpus of the data the language model is trained on. This training requires a lot of computational resources and unstructured data. LLMs came into existence after the release of the sequence-to-sequence models known as **Transformers**.  
  
Transformers model released in 2017 in a paper named **"Attention is all you need"**: This paper was released by Google researchers, and it has achieved more than 38k+ citations in just 5+ years. Before we proceed with LLMs and their working, let's understand how a model learns a language.  
  
Before we proceed with LLMs and its working, let's understand on how a model learns and understand language.

## Information theory and Word Representations

### Information theory and Entropy of language

**Information theory** is a field of study within mathematics and computer science that deals with quantifying the amount of information present in a message or data. It was developed by **Claude Shannon** in the 1940s and has since become a fundamental concept in various fields, including NLP. In NLP, information theory and entropy play a crucial role in understanding the complexity and uncertainty present in natural language data, which helps in developing efficient language models like ChatGPT.

### Intuition for Entropy

Entropy measures the unpredictability or uncertainty present in language data, allowing us to understand the complexity of the language and develop effective language models.  

![](/Image/entropy_formula.png)

  
Let's consider a simple example to understand the importance of entropy in NLP. Suppose we have a small corpus of text containing only three sentences:  

- **AI Planet's LLM Bootcamp**
- **LLM Bootcamp is free**

  
Now, let's calculate the entropy of the words in this corpus.  
  
Calculate the probabilities of each word occurring: - Probability of "AI": 1/8 - Probability of "Planet's": 1/8 - Probability of "LLM": 2/8 - Probability of "Bootcamp": 2/8 - Probability of "is": 1/8 - Probability of "free": 1/8  
![](/Image/entropy_example.png)
  
This positive value indicates that the language in this corpus is somewhat diverse, and there is some unpredictability in the dataset. With only a small number of unique words and a relatively small dataset, the entropy is still relatively low compared to larger and more diverse corpora.  
  
Entropy is a crucial concept in information theory and plays a significant role in natural language processing (NLP). It helps quantify the unpredictability and complexity of language data. Higher entropy values are expected when dealing with larger and more diverse corpora, where the language data contains a wider range of words and is more unpredictable.

### Word Representations

The word or text data in general is processed and analyzed at the level of tokens and word representations. Tokenization involves breaking down a piece of text into smaller units called tokens, which can be as short as a character or as long as a word or group of words. A model only understand numerical representation. Once the tokenization is performed converting words into numerical formats is in the next step.

#### One Hot Encoding

One Hot encoding is a Word representation technique used to represent words in a numerical format. In this encoding method, each word in a vocabulary is represented as a binary vector(0 or 1), where all elements are zero except for the index that corresponds to the word's position in the vocabulary, which is set to one.  
  
For example, let's consider a small vocabulary with four words: "LLM", "GenAI", "NLP" and "ML" The One Hot encoding representation for these words would be as follows:

- LLM → [1, 0, 0, 0]
- GenAI → [0, 1, 0, 0]
- NLP → [0, 0, 1, 0]
- ML → [0, 0, 0, 1]

One Hot encoding has some limitations, especially when dealing with large vocabularies, as it results in very high-dimensional and sparse vectors. This can lead to computational inefficiency and difficulty in capturing semantic relationships between words. Additionally, One Hot encoding treats each word as independent and does not take into account the relationships and similarities between words.  
To address these issues, word embeddings were introduced.  

#### Word Embeddings

Word embeddings are dense, low-dimensional vector representations of words, which are learned from large amounts of text data using techniques like Word2Vec, GloVe, or FastText. These embeddings aim to capture semantic and syntactic relationships between words, which provides better understanding and meaning for the context of words in the data.

Let's take an example to illustrate the power of word embeddings. Consider the following sentences:

- **The queen sits on the throne.**
- **The king sits on the throne.**

With One Hot encoding, the word "queen" and "king" would be represented as completely different, independent vectors, making it challenging to understand their similarities. However, with word embeddings, these words might be represented as follows:

- **queen** → [0.83, 0.12, -0.45, ...]
- **king** → [0.81, 0.15, -0.42, ...]

Here, you can see that the word embeddings for "queen" and "king" have similar values in some dimensions, indicating that they share some semantic similarities.

Word embeddings have significantly improved the performance of various NLP tasks, including sentiment analysis, machine translation, and question-answering systems, by allowing models to better understand the meaning and context of words in a more efficient and effective way compared to One Hot encoding.

## N-grams and Bag of Words in Language models

### N-grams:

Imagine you're reading a book and you want to understand how words are related to each other. N-grams are like puzzle pieces that help us piece together the language puzzle. An N-gram is a sequence of 'N' consecutive words in a sentence or text. For example, let's take the sentence "The cat is sleeping on the sofa."

- A 1-gram (also called unigram) would be: "The", "cat", "is", "sleeping", "on", "the", "sofa".
- A 2-gram (bigram) would be: "The cat", "cat is", "is sleeping", "sleeping on", "on the", "the sofa".
- A 3-gram (trigram) would be: "The cat is", "cat is sleeping", "is sleeping on", "sleeping on the", "on the sofa".

N-grams help us capture some context and structure in language. They are useful in tasks like language modeling, where we predict the likelihood of a word given the previous N-1 words. N-grams also play a role in machine translation, speech recognition, and more. However, they have limitations – as the value of 'N' increases, we might encounter data sparsity issues and miss out on capturing long-range dependencies.

### Bag of Words (BoW):

Think of a Bag of Words like a mixed-up bag of colorful candies. In this case, the candies are words, and we don't care about the order they're in – we just care about which candies are in the bag. The Bag of Words model simplifies text by treating each document or sentence as a collection of words, ignoring grammar and word order.

#### Here's how it works:

We create a vocabulary of all unique words in our corpus (collection of texts). For each document, we count how many times each word appears. We represent each document as a vector, where each entry corresponds to the count of a specific word.  
The Bag of Words model is used in tasks like document classification, sentiment analysis, and information retrieval. It helps us analyze and compare texts by focusing on their essential components – the words they contain.  
  
N-grams and Bag of Words serve as essential tools to help computers understand and process human language. They might seem simple, but they form the foundation upon which more advanced models are built. By grasping the relationships between words and capturing the basic structure of text, we're able to make sense of the vast and complex world of language.

## Overview: How do Large Language Models work?
  
![Transformer Architecture](/Image/transformer_architecture.png)

In the conclusion of Day 1 to the LLM bootcamp, let's understand how a Large Language Models work.  
  
In general, Large Language models are a Transformer models on a large scale. To train such model a huge amount of data is needed. During training, the model learns to assign different weights to different words in a sentence, allowing it to understand the context and relationships between words. This enables the model to generate coherent and contextually appropriate responses to various input queries.  

### But what makes LLM different from Transformers?

Transformers are a specific architecture used in NLP, while Large Language Models are a broader category of models that utilize the Transformer architecture but are distinguished by their massive size and parameter count, leading to enhanced language understanding and generation capabilities.  
  
Furthermore, LLM are classified as Autoregressive models. An Autoregressive approach means that the model generates text one word or token at a time, with each word being conditioned on the previous words in the sequence.  
  
For instance, when you provide an initial prompt to an autoregressive LLM, it processes the prompt and predicts the next word in the sequence based on the context of the prompt. Once it predicts the next word, it uses this word along with the previous context to predict the subsequent word. This process continues iteratively until the desired length of text is generated.  
  
Further in this Bootcamp, you will gain insights on Transformers and its working, which will then give you better understanding of such models.

Don't forget to work on Quickstart guide to PyTorch basics.

## Related Notes

## References
