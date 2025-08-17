---
layout: page
title: Modelling Human Attention
description: A transformer-based system that predicts the most engaging moments in YouTube videos.
img: assets/img/4.png
importance: 4
---

#### Introduction

_Modelling Human Attention_ is a research project where I built a transformer-based system to predict which parts of a video are most engaging to viewers — using only the video transcripts. The idea was inspired by YouTube’s _Most Replayed_ feature, which highlights moments people tend to watch again.

#### Problem

While replay peaks are a strong signal of engagement, they are only available after a video has been watched many times. This makes it impossible for creators, advertisers, or platforms to know which segments will be replayed before release. Additionally, replay data is often noisy — influenced by random skipping, incomplete transcripts, and differences in content style.

#### Approach

I designed a **peak-driven segmentation strategy** to split transcripts into meaningful chunks aligned with viewer attention patterns.

- **Bias Correction** for inflated early peaks.
- **Adaptive Thresholds** to detect both strong and subtle moments of engagement.
- **Semantic Coherence** so each segment contains a complete, meaningful idea.

These segments were processed using a transformer architecture that combined:

- **Local Context** — the segment’s own text.
- **Global Context** — video title and summary.
- **Genre Embeddings** — to adapt to different video styles.

The model was trained with focal loss to handle class imbalance between “peak” and “non-peak” segments.

#### Results

- Achieved **high replay peak prediction accuracy** across multiple genres.
- Sports and Technology content showed the strongest predictability.
- The model performed well **even without replay data** at inference, using only transcript content.

#### Key Findings

- Engagement cues are embedded in language patterns, especially in sports commentary and tech reviews.
- Different genres have different optimal segmentation granularities.
- Coarser segmentation works better for narrative-rich content; finer segmentation benefits structured educational content.

#### What I Solved

I created a method to **predict viewer engagement before a video is published**, using only its transcript. This solves the problem of needing post-release replay data and makes engagement prediction more accessible and scalable.

#### Conclusion

By fusing textual, contextual, and genre-based features, this project demonstrates that viewer attention patterns can be modeled reliably without visual or audio cues. This opens possibilities for content optimization, targeted advertising, and personalized recommendations.

#### Future Improvements

- Add **multimodal signals** (audio tone, visual motion) for richer engagement detection.
- Develop an **adaptive segmentation algorithm** that automatically chooses segment size per content type.
- Expand testing on short-form and multilingual content.
