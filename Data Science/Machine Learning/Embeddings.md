Embeddings are numerical representations of words or phrases that capture their meaning and context. They allow NLP algorithms to process language more effectively and accurately.

## Importance of Embeddings in NLP

In NLP, the goal is to create models that can understand and process language in a way that is similar to how humans do. However, unlike humans, computers cannot understand language directly. They need a way to represent language in a numerical format. This is where embeddings play a crucial role.

Embeddings capture the meaning of words in a numerical format that can be easily processed by algorithms. They allow NLP models to understand the relationships between words and phrases, and to recognize patterns in language. Without embeddings, NLP models would struggle to accurately interpret language and produce meaningful results.

## Different Embedding Techniques

There are several different techniques used to create embeddings in NLP. Here are some of the most common ones:

1. **Bag of Words**
	The bag of words technique is one of the simplest ways to create embeddings. It works by counting the frequency of each word in a text corpus and creating a vector for each word. The resulting vectors can be used to represent the words in a numerical format that can be easily processed by algorithms. However, this technique does not capture the meaning or context of words, which limits its usefulness.
	
	The bag of words technique can be represented mathematically as follows:

	Let $D$ be a corpus of documents, and let $V$ be the vocabulary of words in $D$. Then, for each document $d$ in $D$, we create a vector $x(d)$ of length $|V|$, where each element in the vector represents the count of a word in $V$ in the document $d$.
	
	$x(d)_i$ = number of occurrences of the word $i$ in document $d$
	
	This creates a matrix $X$ of size $|D|$ x $|V|$, where each row represents a document and each column represents a word in the vocabulary.

2. **Word2Vec**
	Word2Vec is a popular embedding technique that was introduced by Google in 2013. It works by training a neural network to predict the context of a word based on its surrounding words. The resulting embeddings capture the meaning and context of words, which makes them more useful than bag of words embeddings.
	
	![[Pasted image 20230301202920.png]]
	
	Word2Vec can be represented mathematically using a neural network model. The basic idea is to predict the probability of a word appearing in the context of another word.
	
	Let $w_t$ be a target word and $w_c$ be a context word. We use a neural network with a single hidden layer to predict the probability of $w_c$ given $w_t$. The input layer of the neural network consists of one-hot encoded vectors representing each word in the vocabulary. The output layer consists of a softmax function that outputs the probability distribution over all words in the vocabulary. The hidden layer represents the word embedding.

3. **GloVe**
	GloVe, which stands for Global Vectors for Word Representation, is an embedding technique that was introduced in 2014. It works by creating a co-occurrence matrix that captures the frequency of words appearing together in a text corpus. The resulting embeddings capture both the meaning and context of words, which makes them highly effective for NLP tasks.
	
	GloVe creates word embeddings by factorizing a matrix of word co-occurrence statistics. The basic idea is that the meaning of a word can be captured by the context in which it appears.
	![[Pasted image 20230301202940.png]]

4. **BERT**
	**BERT** is a transformer-based model that creates contextualized embeddings. The basic idea is to use a transformer encoder to generate a representation of a sentence or a document that captures the meaning and context of each word.
	
	Let $S$ be a sentence or a document. We first add special tokens `[CLS]` and `[SEP]` to the beginning and end of the sentence, respectively. We then use a transformer encoder to generate a representation of each token in the sentence.
	![[Pasted image 20230301203109.png]]

5. **FastText**
	FastText is a technique that extends the Word2Vec model by representing words as a bag of character n-grams. This allows the model to capture the morphology of words.
	![[Pasted image 20230301203141.png]]

6. **ELMo (Embeddings from Language Models)**
	ELMo is another transformer-based model that creates contextualized embeddings. The basic idea is to use a bi-directional LSTM to generate a representation of each word that takes into account the context to the left and right of the word.
	
	Let S be a sentence or a document. We use a bi-directional LSTM to generate a representation of each word in the sentence. We concatenate the forward and backward LSTM hidden states for each word to get a final representation that captures the meaning and context of the word.
	
	The objective function for ELMo is a language modeling task, where we ask the model to predict the next word in a sentence given the previous words.
	![[Elmo_embedding.gif]]

7. **Transformer-XL**
	
	Transformer-XL is another transformer-based model that creates contextualized embeddings. The basic idea is to use a segment-level recurrence mechanism to generate representations that capture longer-term dependencies.
	
	Let S be a sentence or a document. We use a transformer encoder to generate a representation of each token in the sentence. We also use a segment-level recurrence mechanism that allows the model to reuse previously computed hidden states to capture longer-term dependencies.
	
	The objective function for Transformer-XL is a permutation language modeling task, where we ask the model to predict the next word in a randomly ordered sequence of tokens.
	
	![[Pasted image 20230301203446.png]]

8.  Universal Sentence Encoder (USE)
	
	The Universal Sentence Encoder is a pre-trained encoder model developed by Google that generates high-quality sentence embeddings. The model is trained on a large amount of text data and is capable of handling a wide range of natural language processing tasks, including sentiment analysis, question answering, and text classification.
	
	One of the key features of USE is that it can handle out-of-vocabulary words well, meaning that it can generate embeddings for words that it has not seen before. This is because the model incorporates subword information into its embeddings.
	
	The USE model consists of two variants: one that uses a transformer-based architecture (USE-T), and one that uses a deep averaging network (USE-D). Both variants generate embeddings that are 512-dimensional vectors.

9.  Sentence-BERT
	
	Sentence-BERT is a technique for generating high-quality sentence embeddings that was introduced in a 2019 paper by Reimers and Gurevych. The method is based on the popular BERT (Bidirectional Encoder Representations from Transformers) model, which is a transformer-based neural network architecture that generates contextualized embeddings for words.
	
	To use BERT for sentence embeddings, Sentence-BERT fine-tunes the pre-trained BERT model on a dataset of sentence pairs with the objective of maximizing the similarity between embeddings of semantically similar sentences and minimizing the similarity between embeddings of semantically dissimilar sentences.
	
	The resulting Sentence-BERT model generates sentence embeddings that are 768-dimensional vectors, which are much larger than those generated by USE. However, Sentence-BERT tends to produce higher-quality embeddings than USE, particularly for tasks that require capturing more subtle semantic relationships between sentences.
	
	Overall, both USE and Sentence-BERT are powerful techniques for generating sentence embeddings, and the choice between the two depends on the specific needs of a given NLP task.