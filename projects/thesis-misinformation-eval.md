---
layout: project
type: project
image: ""
placeholder: true
title: "Multi-Agent LLM Misinformation Evaluation"
date: 2026
published: true
featured: true
labels:
  - LLM Agents
  - Python
  - Flask
  - SQLite
  - Evaluation
summary: "M.S. thesis research: a 5-agent LLM pipeline for detecting misinformation in social media posts, rigorously evaluated against human ground truth."
---

<div class="pf-placeholder">
  <div>
    <span class="pf-placeholder-label">Screenshot placeholder</span>
    Annotation tool UI — to be added
  </div>
</div>

<hr>

## Introduction
<p>
For my M.S. thesis, I'm designing and rigorously evaluating a multi-agent LLM system for detecting misinformation in social media posts. The core question isn't just "can agents catch misinformation?" — it's "how do we actually know if they're working, and at what cost?" To answer that, I built an evaluation harness that scores competing systems against human ground truth using both deterministic metrics and an LLM-as-judge model.
</p>

## The 5-Agent Pipeline
<p>
Rather than relying on a single frontier model to do everything, I designed a 5-agent specialist pipeline — OCR, fact-checking, media forensics, context analysis, and linguistic analysis — to test whether decomposing the task across smaller, cheaper models could match or exceed a single frontier model's accuracy at a fraction of the inference cost. In practice, that pipeline runs at roughly <span class="pf-mono">$0.025–$0.396 per post</span>, depending on complexity.
</p>

## From Prompts to Code
<p>
Early on, agent reliability failures kept slipping through — models would occasionally make overconfident claims without sufficient evidence. Prompt-only fixes (asking the model more firmly to cite evidence) weren't reliable enough, so I moved enforcement out of the prompt and into code: explicit evidence gates and automatic confidence downgrades when an agent's claims aren't backed by retrieved evidence. That shift from "ask nicely" to "verify programmatically" made the pipeline meaningfully more trustworthy.
</p>

## Building Ground Truth
<p>
Good evaluation needs good labels, so I built a Flask and SQLite human-annotation web application to generate ground-truth data — indexing an <span class="pf-mono">811MB</span> label-history corpus and <span class="pf-mono">2.85M</span> filtered records with resumable checkpointing, producing <span class="pf-mono">713</span> human annotations and <span class="pf-mono">102</span> curated ground-truth records.
</p>

## Judging the Judges
<p>
The LLM-as-judge scoring phase is deliberately drawn from a different model family than the systems it grades, specifically to catch overconfident or unsupported claims that a same-family judge might be more likely to let slide. This is the part of the project I find most interesting: it's not just about building agents that seem to work, it's about proving whether they actually do — and being honest about what that proof costs.
</p>

## Status
<p>
This work is ongoing as part of my M.S. thesis at the University of Hawai'i at Mānoa. I'll be updating this page with results and a link to the published thesis as the work progresses.
</p>
