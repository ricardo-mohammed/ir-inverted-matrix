> **For the instructor:** The completed solution is in [`notebooks/InvertedMatrix_Group3_Solution.ipynb`](notebooks/InvertedMatrix_Group3_Solution.ipynb).

# PROG8245: Inverted Matrix & Information Retrieval Workshop

**Class:** PROG8245 - Applied AI & Machine Learning<br>
**Assignment:** Inverted Index, Positional Indexes, and TF-IDF Implementation<br>
**Date:** November 24, 2026

## Team 3

| Name | Student ID |
| :--- | :--- |
| Ricardo Mohammed | 7500382 |
| Juan Camilo Chirivi | 9115141 |
| Zeynep Ozdemir | 9045142 |
| Senay Teweldebrhan | 9120588 |

## Project Overview

The notebook implements an Information Retrieval (IR) pipeline, from document collection and linguistic preprocessing through inverted and positional indexing, Boolean and phrase queries, and TF-IDF document ranking. It also discusses how these traditional IR techniques support modern applications such as Retrieval-Augmented Generation (RAG) and AI agents.

## Setup

The notebook was developed with Python 3.12. From the repository root, create and activate a virtual environment:

**Windows (PowerShell):**

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

**macOS/Linux:**

```bash
python3 -m venv .venv
source .venv/bin/activate
```

Install the project dependencies and start Jupyter:

```bash
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
jupyter lab
```

Open [`notebooks/InvertedMatrix_Group3_Solution.ipynb`](notebooks/InvertedMatrix_Group3_Solution.ipynb) in JupyterLab and run its cells from top to bottom. On its first run, the notebook downloads the NLTK movie-review corpus, English stop words, and tokenizer data.

## Analysis Summary

### Corpus and preprocessing

The notebook uses the first 100 reviews from NLTK's `movie_reviews` corpus. This subset keeps indexing quick while providing enough variety for the assignment's vocabulary requirement. Text is lowercased, tokenized with a word-based regular expression, filtered using NLTK's English stop-word list, and normalized with the Porter Stemmer. The processed subset contains **6,795 unique terms**, exceeding the 2,000-term target.

### Inverted index and Boolean retrieval

The inverted index maps each stemmed term to the document IDs in which it appears. Each document contributes a term only once to a posting list, so the index supports efficient document-level lookup. Boolean AND is implemented as a posting-list intersection; AND NOT uses set difference. In the notebook's examples, `movie` (stemmed to `movi`) appears in **87** reviews, while the `movie AND great` query matches **18** reviews.

### Positional index and phrase search

Alongside the document-level index, a positional index records each token's location in each review. Phrase queries preprocess the phrase, find documents containing every query token, and then check that the tokens occur at consecutive positions in the requested order. For example, `bad movie` matches **5** reviews and `good story` matches **2**. This position-aware check distinguishes exact phrases from documents that merely contain the same words in a different order.

### TF-IDF ranking and IR in AI

The notebook ranks documents with a manually computed query score: each query term's raw frequency in a document is multiplied by its inverse document frequency, `log(N / df)`, where `N` is the corpus size and `df` is the number of reviews containing the term. Scores are summed across query terms and sorted in descending order. For `bad movie`, the top results are reviews 13, 9, and 27, with scores of **5.1868**, **4.6808**, and **4.5416**, respectively.

The discussion connects these methods to hybrid RAG: vector retrieval can find semantically related passages, while sparse term indexes and positional matching provide exact keyword and phrase retrieval. The notebook also notes practical trade-offs, including the speed and compactness benefits of optimized posting lists, and the difference between fast stemming and linguistically richer lemmatization.

## AI Use Disclosure

AI tools were used to assist with implementation of this project.