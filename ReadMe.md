# Movie Recommendation System using Locality Sensitive Hashing (LSH)

## Overview

This project is a movie recommendation system built using Natural Language Processing techniques and **Locality Sensitive Hashing (LSH)**. The goal is to recommend ten movies similar to a given input movie by analyzing movie metadata from the Rotten Tomatoes dataset.

## Table of Contents

- [Motivation](#motivation)
- [Dataset](#dataset)
- [Preprocessing](#preprocessing)
- [Modeling Approach](#modeling-approach)
- [Results](#results)
- [Technologies Used](#technologies-used)
- [Team](#team)
- [Future Work](#future-work)

---

## Motivation

With thousands of movies available on streaming platforms, viewers often need help finding similar movies they’d enjoy. Our model aims to suggest movies based on similarity in metadata such as genre, director, cast, and plot description—_not_ just popularity. LSH is used to provide fast and scalable recommendations.

---

## Dataset

We used the **Rotten Tomatoes Movies and Critic Reviews** dataset from Kaggle:
[https://www.kaggle.com/datasets/stefanoleone992/rotten-tomatoes-movies-and-critic-reviews-dataset](https://www.kaggle.com/datasets/stefanoleone992/rotten-tomatoes-movies-and-critic-reviews-dataset)

**Key features used:**

- `movie_title`
- `movie_info` (reduced using TF-IDF)
- `content_rating`
- `genres`
- `directors` (limited to primary)
- `actors` (top 4 per movie)

---

## Preprocessing

Steps included:

- Removed irrelevant columns and rows with critical null values.
- Normalized movie titles, genres, actor and director names.
- Applied TF-IDF to reduce and focus `movie_info`.
- Concatenated relevant features into a single column (`movie_combined`).
- Created genre-guided shingles for LSH input.

---

## Modeling Approach

- **Shingling**: Created `k=2` shingles combining each genre with tokens from `movie_combined`.
- **MinHashing**: Used 1024 permutations to generate compact signatures.
- **LSH Forest**: Indexed MinHash signatures for efficient Jaccard-based similarity search.
- **Recommendation**: Given an input movie, generated 10 most similar movie suggestions using approximate nearest neighbor search.

---

## Results

Examples:

- Input: `Avengers: Age of Ultron`
  Output: Other Marvel films like _Infinity War_, _Civil War_, _Thor: The Dark World_.
- Input: `The Hangover`
  Output: Sequels and other Bradley Cooper comedies like _Silver Linings Playbook_.

While the model is unsupervised, evaluation was done through human interpretability and semantic similarity.

---

## Technologies Used

- Python
- Pandas, NumPy
- Scikit-learn (TF-IDF)
- SpaCy (NLP preprocessing)
- Datasketch (MinHash, LSH Forest)

---

## Team

- **Laert Xhumari** - https://github.com/LaertXh
- **Wendy Ralston** - https://github.com/ala-hajjar
- **Alaa El Hajjar** - https://github.com/weralston

> This project was developed as part of the CIS 9665 NLP course at Baruch College.
