---
layout: page
title: Direct Preference Optimization (DPO)
description: Implemented and analyzed Direct Preference Optimization on the Anthropic-HH dataset, studying sensitivity to KL temperature and observing reward collapse regimes.
img: assets/projects/academic/DPO/DPO.png
importance: 3
category: academic projects
github: https://github.com/rubenifrah/DPO-implementation-and-finetuning
tags: [LLM, deep learning, research]
---

This project explores **Direct Preference Optimization (DPO)** as a stable and efficient alternative to Reinforcement Learning from Human Feedback (RLHF) for aligning Large Language Models (LLMs) with human preferences.

It is part of our final assignement with colleague Rebecca El Chidiac (fellow Polyetchnique student) for the course "Large Language Models" by **Alexandre Allauzen** and **Florian Le Bronnec**.

The idea was to implement the full DPO pipeline and bring a relevant study to the table. We decided to conduct a hyperparameter study to find the best beta value for the DPO alignment process.

The results show that a beta value of 0.1 is the best for the DPO alignment process, as recommended by the authors of the paper.

[Direct Preference Optimization:Your Language Model is Secretly a Reward Model](https://arxiv.org/pdf/2305.18290) (reference article)

[Read our full report (PDF)](/assets/projects/academic/DPO/DPO_report.pdf)

[View our presentation slides (PDF)](/assets/projects/academic/DPO/DPO_presentation.pdf)
