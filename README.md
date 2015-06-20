# Text Categorization using Graph of Words approach vs. Bag of Words approach

## Introduction
The goal of this project is to classify a certain number of texts, using a Vector Space Model, which is a spatial representation of documents. Each document can be described as a vector with a certain number of features, each feature corresponding to a specific word in a training vocabulary set.
The dataset used is the preprocessed Reuters dataset, which contains 5,495 training documents and 2,189 testing documents, with 8 different labels. Preprocessing has been used so as to apply tokenization, stop-words removal and stemming to the initial texts.
The idea behind the approaches described in the notebook is to construct ”smart” Document-Term matrices, i.e matrices of size n×m, where n is the number of documents and m the number of features, chosing the ”right” weights to fill in these matrices. ”Good” weights will allow to discriminate between the different text labels, and will be of great help to whatever learning algorithm will be used.

## Bag of Words vs. Graph of Words
In the usual bag of Words Representation, the order between different words in a text is not taken into account ; it has been built here using TfidfVectorizer.
As opposed to the Bag of Words Representation, the Graph of Words representation captures the relationships between the words according to their positions within the text. Each document is represented as a graph, the words being the nodes, and the edges being the relationships among them. Here, we build an edge between two given words, if they both appear within a window of a given size.

The important parameters taken into account in the representation are :
— Directed or undirected graphs, via the parameter isdirected — Weighted or unweighted graphs, via the parameter isweighted — The size of the window, via the parameter size window
— The centrality measure, equal to ’pagerank’ or ’degree’

The approach used here has been proposed as an extension of Vazirgiannis and Rousseau's work, in http://www.lix.polytechnique.fr/~rousseau/papers/rousseau-cikm2013.pdf.
The idea is to build the term-weights (TW) for each document by using a centrality measure on the graph of words of the document, and, as compared with the TFIDF approach, to multiply these weights by a graph-based IDF value for each term. This graph-based IDF value for each word can be computed as a centrality measure of this term on the overall graph formed by all the training documents.

## Packages

The networkx (1.9.1) Python package is used to build the graphs of words, while scikit-learn (0.16.0) is used to train and test the different classifiers.