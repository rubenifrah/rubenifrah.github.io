---
layout: page
title: Spotify Recommender System
description: A personalized music taste modeling pipeline using XGBoost and Spotify API.
img: /assets/projects/spotify/PCA_2D.png
importance: 2
category: personal projects
github: https://github.com/rubenifrah/spotify-recommender
giscus_comments: true
tags: [Data, deep-learning]
---

A complete, modular, production‑grade pipeline that learns **your personal musical taste** using a large Kaggle Spotify dataset and your own liked songs exported from Spotify.

The project trains a classifier (XGBoost) to predict the probability that you will like a new song based on audio features, genre embeddings, and historical preferences. It also produces visualizations, PCA embeddings, feature importance plots, balanced datasets, and a fully reproducible recommendation pipeline.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/projects/spotify/features_distribution.png" title="Feature Distribution" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/projects/spotify/correlation_matrix.png" title="Correlation Matrix" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: Feature distribution of liked vs non-liked songs. Right: Correlation matrix of audio features.
</div>

## Key Features

*   **Personalization**: The learned decision boundary reflects *my* musical preferences, not the crowd’s.
*   **Discovery**: The model identifies songs I am likely to love **but have never heard**, enabling genuine exploration.
*   **Interpretability**: The modeling pipeline reveals whether my taste is driven by acoustic properties (valence, tempo, energy) or cultural/contextual factors (genre, popularity, release year).

## Methodology

### Data Engineering & Custom Balancing
Two sources are merged: a Kaggle dataset with tens of thousands of tracks and my personal liked songs (~1899 tracks).
A binary target is created (`liked = 1` if track_id ∈ my liked songs, `0` otherwise).

To handle the severe class imbalance (~1,900 liked vs >150,000 not-liked), I implemented a custom balancing strategy:
*   **Oversampling**: Synthetic “liked” examples are created by finding non‑liked songs by frequently liked artists and selecting acoustically similar tracks.
*   **Undersampling**: The majority class is randomly reduced to produce a **2:1 ratio** of not‑liked to liked.

### Feature Engineering
Spotify’s ultra‑granular `track_genre` field is condensed into **10 macrogenres** (pop, rock, electronic, etc.) to improve generalization and interpretability.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/projects/spotify/feature_importance.png" title="Feature Importance" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    XGBoost Feature Importance: Contextual factors like popularity and release year play a major role alongside audio features.
</div>

## Modeling & Results

I evaluated multiple models (XGBoost, MLP, Random Forest) and selected **XGBoost** for its robustness and interpretability.
After hyperparameter tuning (GridSearchCV with 5-fold CV), the model achieved a **Weighted F1-score of 0.93**.

*   **Precision (Liked)**: 0.89
*   **Recall (Liked)**: 0.84

## Visualizations

The PCA projections reveal that liked songs cluster in two major regions (energetic/upbeat and calm/atmospheric), while non-liked songs are widely dispersed.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/projects/spotify/PCA_2D.png" title="PCA 2D" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/projects/spotify/PCA_by_genre.png" title="PCA by Genre" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

## Tech Stack
*   **Languages**: Python
*   **Libraries**: Pandas, Scikit-learn, XGBoost, Spotify API
*   **Tools**: Git, Makefile, Unit Tests
