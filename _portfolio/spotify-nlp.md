---
title:  "Spotify Music Recommendation System "
excerpt: "Exploring semantic relationships between lyrics"
collection: portfolio
---

## Overview
Developed a machine learning recommendation system that suggests songs based on their lyrics. 
Rather than relying on a single modeling approach, the project explored multiple recommendation techniques, feature representations, and preprocessing strategies to determine which methods produced the most meaningful recommendations.

## Problem
Recommendation systems power many modern digital platforms, from music streaming services to e-commerce and video platforms. 
The objective of this project was to investigate how different machine learning techniques and feature engineering decisions influence the quality of personalized music recommendations.

## Dataset
- My personal liked songs on Spotify
    - ~2,000 songs spanning all genres
- Lyrics of my liked songs extracted via the Genius API

## Methodology
Instead of committing to a single solution, the project compared multiple approaches for generating recommendations. 
Models:
- TF-IDF
- TF-IDF (chorus only)
- LSA
- LyricsBERT

All models were testing on the same genres and seed songs:
- **Grunge**: Iron Clad Lou — Hum
- **Soul**: Everybody Loves The Sunshine — Roy Ayers Ubiquity
- **Latin**: Volare — Gipsy Kings
- **Hip-hop**: House Money - Baby Keem

Modeling was done iteratively to capture differences in increasingly dense embeddings. 

## Results
Across all models, performance was generally low indicating lyrics alone is not a good system of song recommendation. 
However, there was a consistent pattern across all models in which the similarity scores for the latin and hip-hop genres were exceedingly higher than soul and grunge across all models. 
Leading to the conclusion that soul and grunge are better identified by their musical composition while latin and hip-hop have more repetitive verbiage. 
Hip-hop exemplified these results the best as it had the highest similarities scores across all models due to its repetitive adlibs and explicatives.

## Technical Challenges
Some of the most significant engineering challenges included:
- Working with the Spotify API (it is heavily depreceated)
- Exacting only the chorus from every song in my dataset
- Quantifying the results between genres


## Repository

[View Code](https://github.com/joe-ledford-04/NLP-Final-Project-Spring-2026)
