---
layout: post
title:  "Learning Video-Native Self-Supervised Representations"
date:   2024-11-10 15:11:55 -0700
categories: research ideas
---
*Or: Is a video worth more than a thousand photos?*  

**TLDR:** Current video [retrieval](https://arxiv.org/pdf/2305.05665)/[understanding](https://llava-vl.github.io/blog/2024-04-30-llava-next-video/) solutions differ fundamentally from those for video [generation](https://arxiv.org/abs/2407.01392) in their treatment of temporal information. Can carefully integrating time into our video representations allow us to understand causal relationships that can’t be computed from image embeddings alone? How do we design self-supervised learning algorithms that let our models learn these representations “natively,” integrating information more effectively than a model that processes images alone?

Consider a “bag of images” model, an image model which embeds all frames of a video independently, and takes the mean across frames to compute an embedding of the video. Such a model would be fairly performant on tasks like naive text-based retrieval; however, it would destroy so much information\! It wouldn’t know if a clip was playing forward or backward, or if gravity pointed up or down, or if firefighters using water hoses started fires. Current SOTA approaches (like [CLIP2Video](https://arxiv.org/abs/2106.11097)) are more sophisticated (although only slightly more performant) than this baseline; they still rely heavily on rich image representations learned independently from video, alongside “shallow” temporal modules. *The real world is governed by cause and effect. Time only flows one way. Why don’t our representations reflect this reality?*

Previous work ([MERLOT](https://arxiv.org/pdf/2106.02636)) *has tried* to learn temporal relationships using frame ordering as a classification loss term for self-supervised learning. In their case, it didn't help downstream fine-tuning performance on datasets like TVQA: likely due to their testing methodology (5 to 7 consecutive frames is too fast). Thus, **novel evaluations** are necessary for testing video representations for temporal coherence and causal understanding.

Inspired by work on SSL in the image domain (e.g., DINO), there is a wide range of possible benchmarks to determine feature quality. Some preliminary ideas include predicting physical properties that rely on the unidirectional nature of time (e.g., gravity, entropy), directly modeling cause-effect relationships via “predictive” VQA, or even directly predicting and retrieving future clips.

I strongly believe that videos are more than the sum of their frames. As an engineer, I want to train foundation models in ways that let them understand time “natively” and write the evaluations that will test for such understanding. As an interpretability researcher, I want to work on finding the [time vectors](https://arxiv.org/abs/2312.13401) in the geometry of such models’ representation spaces. I’m excited to build systems that learn to model the arrow of time from scratch on internet-scale data.

Thanks to [Ali Cy](https://www.ali.cy/) for the helpful discussions that inspired this document. 