---
layout: post
title: "Recommender Systems III"
date: 2022-05-28
categories: [data-science]
usemathjax: true
---

## General

### Where we focus

- User-Item Recommendation
- Item-Item Recommendation
  - **Content based recommendation**
  - **Collaborative Filtering**

### Recall: Notes on Item-Item Recommendations

- recommendation based on last item: *"If you are interested in this, you probably also like ..."*
- doesn't need a user model
- Item model needed → How to model similarities between items?

### Recall: Collaborative Filter

...

...

....

### Content based Recommendation

- we have more information about the film than just a number, we know the content of the film → how to find similar items based on item properties and/or meta data?

Possible solutions:

- Compute distance between movies for example (e.g. calculate sequences) → possible with DL, but too expensive in most cases
- use meta data → Categorization, actors/directors, year, ...
- use simpler measure → e.g. analyze movie poster

### Recall: Benefits of DL

- capacity of the learned mapping → tensor input/output, like pictures, videos, tables, ...

<div style="text-align:center">
<img src="/wp-content/uploads/2022/05/Screenshot-2022-05-05-at-13.39.01.png" alt="DL tensor input/output mapping" style="width: 70%; height: auto;">
</div>

- End-to-End Learning → learn decision space and function in one optimization problem

<div style="text-align:center">
<img src="/wp-content/uploads/2022/05/Screenshot-2022-05-05-at-13.40.12.png" alt="End-to-End Learning" style="width: 70%; height: auto;">
</div>

## Different Approaches of using DL in Recommender Systems

### Autoencoder

- instead of a SVD a non-linear operation to compress data
- consists of two parts:
  - encoder → compresses data in a latent space
  - Decoder →
- we measure the distances in the compressed space
- we can add additional evaluations to our loss function based on previous ratings

### Basic CNN Approach

- Use CNNs for item (and user) content feature extraction
- Examples:
  - Movie similarity by image similarity of posters
  - Clothing and fashion items, e.g. I like this kind heel, suggest me other shoes that have a similar heel
- can directly combined with AE or SVD

### RNN based Recommender Systems

- **Using RNNs for text feature extraction:**

1. User features: reviews and comments by a user → if somebody often insults, a negative rating doesn't value much → if somebody only writes positive things, a negative rating has more impact
2. Item features: text description and reviews of item

<div style="text-align:center">
<img src="/wp-content/uploads/2022/05/Screenshot-2022-05-05-at-19.43.52.png" alt="RNN for text feature extraction" style="width: 70%; height: auto;">
</div>

- s1, s2, ... are words/sequences of the text

### Hybrid Recommender Systems

<div style="text-align:center">
<img src="/wp-content/uploads/2022/05/Screenshot-2022-05-05-at-19.49.06.png" alt="Hybrid Recommender Systems" style="width: 70%; height: auto;">
</div>

Combined Measurements:

- Film poster
- Text (Meta data)
- User Ratings

## Code Exercises

(Links to Github)

[Autoencoder_with_Keras_week8.ipynb](https://github.com/HuberAdrian/DataScience-Lectures/blob/main/Week_8/Autoencoder_with_Keras_week8.ipynb)

[collaborative_filtering_with_Keras_week8.ipynb](https://github.com/HuberAdrian/DataScience-Lectures/blob/main/Week_8/collaborative_filtering_with_Keras_week8.ipynb)