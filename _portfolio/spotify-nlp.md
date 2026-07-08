---
title: "Spotify Lyric Recommendation System"
excerpt: "Comparing classical and transformer-based NLP methods for lyric-based music recommendation."
collection: portfolio
---

## Overview

This project investigates how different Natural Language Processing (NLP) techniques influence the quality of lyric-based music recommendations. Rather than building a single recommendation model, I implemented and compared four independent recommendation pipelines to evaluate how different text representations capture semantic relationships between songs.

The project combines API integration, data engineering, NLP, and similarity modeling to study the strengths and limitations of lyric-based recommendation systems.

## Problem

Commercial music recommendation systems rely on listening history, collaborative filtering, and proprietary user data. This project explores a more constrained problem:

**Can song lyrics alone be used to generate meaningful music recommendations?**

To answer this question, I compared multiple NLP approaches while holding the dataset and evaluation songs constant.

<figure style="text-align: center; margin: 2em 0;">
  <img src="/assets/images/projects/nlp_project/tfidf_vs_lyricBERT.png"
       alt="Comparison of TF-IDF and LyricBERT semantic similarity distributions"
       style="max-width: 100%; border-radius: 6px;">
  <figcaption>
    <strong>Figure.</strong> Distribution of pairwise semantic similarity scores produced by TF-IDF and LyricBERT. While TF-IDF similarities are concentrated near zero, LyricBERT produces a broader distribution that better captures semantic relationships between song lyrics.
  </figcaption>
</figure>

## Dataset

- Approximately 2,000 liked songs from my personal Spotify library
- Song metadata collected through the Spotify Web API
- Lyrics retrieved using the Genius API
- Custom preprocessing pipeline for cleaning and preparing lyric data

## Methodology

Four recommendation models were implemented and evaluated:

- **TF-IDF:** Sparse lexical representation using cosine similarity
- **Chorus TF-IDF:** Evaluated whether restricting lyrics to chorus sections improved recommendations
- **Latent Semantic Analysis (LSA):** Reduced TF-IDF vectors into latent semantic space using Truncated SVD
- **LyricsBERT:** Generated contextual transformer embeddings for semantic similarity

<figure style="text-align: center; margin: 2em 0;">
  <img src="/assets/images/projects/nlp_project/lyricBERT_embedding_space.png"
       alt="LyricBERT embedding space"
       style="max-width: 90%; border-radius: 6px;">
  <figcaption>
    <strong>Figure.</strong> Two-dimensional projection of song embeddings learned by the LyricBERT model.
  </figcaption>
</figure>

Each model was tested using the same seed songs across four genres:

| Genre | Seed Song |
|--------|-----------|
| Grunge | *Iron Clad Lou* — Hum |
| Soul | *Everybody Loves the Sunshine* — Roy Ayers Ubiquity |
| Latin | *Volare* — Gipsy Kings |
| Hip-Hop | *House Money* — Baby Keem |

## Results

The comparison demonstrated that lyrics alone provide limited information for high-quality music recommendation. However, several consistent patterns emerged:

- Hip-hop and Latin music produced higher similarity scores across all models.
- Soul and grunge consistently produced weaker recommendations.
- Transformer embeddings captured richer semantic relationships than traditional vector-space models but remained limited by the information contained solely within lyrics.

These findings suggest that lyrical repetition and vocabulary are stronger signals in certain genres, while others are better characterized by musical composition than textual content.

<figure style="text-align: center; margin: 2em 0;">
  <img src="/assets/images/projects/nlp_project/jaccard_overlap.png"
       alt="Jaccard similarity across genres and recommendation models"
       style="width: 100%; border-radius: 6px;">
  <figcaption>
    <strong>Figure.</strong> Genre overlap between recommendation models measured using the Jaccard similarity metric.
  </figcaption>
</figure>

## Technical Highlights

- Integrated the Spotify and Genius APIs to build a custom lyric dataset
- Implemented four independent NLP recommendation pipelines
- Compared classical vector-space models with transformer embeddings
- Evaluated recommendation quality across multiple genres using a consistent testing methodology

## Repository

[View Source Code](https://github.com/joe-ledford-04/NLP-Final-Project-Spring-2026)
