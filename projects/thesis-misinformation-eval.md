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
  - PyTorch
  - Evaluation
summary: "M.S. thesis research: can a multi-agent debate pipeline make a cheap multimodal model classify misleading X posts as well as stronger single models?"
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
For my M.S. thesis, I'm asking whether an agentic, multi-agent workflow can make a weak, cheap multimodal model classify misleading posts on X as well as newer, stronger single models. "Classify" means two things: deciding <em>whether</em> a post is misleading, and deciding <em>which</em> of seven misinformation types apply (factual error, manipulated media, outdated information, missing context, unverified claim stated as fact, satire, or other). X Community Notes serve as the ground truth. The core question isn't just "can agents catch misinformation?" — it's "how do we actually know if they're working, and at what cost?"
</p>

## The Debate Pipeline
<p>
Rather than relying on a single frontier model, the pipeline runs on a low-cost multimodal backbone (Gemini 2.5 Flash-Lite). Four specialist agents each score the misinformation types they own, then debate over two rounds with a moderator, working from a shared evidence pool gathered for each post. A final verdict agent reads the full debate and decides. I compare two variants: a constrained one, where each specialist may only score its own types, and an unconstrained one, where any agent may score any type.
</p>

## From Prompts to Code
<p>
Early on, agent reliability failures kept slipping through — models would make overconfident claims without sufficient evidence. Prompt-only fixes (asking the model more firmly to cite evidence) weren't reliable enough, so I moved enforcement out of the prompt and into code: about a dozen hard-rule "gates" that strip a flag when it isn't backed by an evidence-pool source or a specialist who scored it, and that judge every post against what was knowable when it was posted. That shift from "ask nicely" to "verify programmatically" made the pipeline meaningfully more trustworthy.
</p>

## Building Ground Truth
<p>
Good evaluation needs good labels, so I built a Flask and SQLite human-annotation web application to generate ground-truth data — indexing an <span class="pf-mono">811MB</span> label-history corpus and <span class="pf-mono">2.85M</span> filtered records with resumable checkpointing, producing <span class="pf-mono">713</span> human annotations and <span class="pf-mono">102</span> curated ground-truth records.
</p>

## Results So Far
<p>
On a 60-post test set (10 posts per misinformation type), the cheap debate pipeline found the labeled type on <span class="pf-mono">60%</span> of posts, against <span class="pf-mono">53%</span> for the strongest single model (GPT-5.6), at about a third of the cost (<span class="pf-mono">$0.83</span> vs. <span class="pf-mono">$2.25</span> per 60 posts). The difference isn't statistically significant, so the honest claim is that the pipeline <em>matches</em> the stronger model on recall. Where it falls behind is precision: it raises significantly more extra types per post.
</p>
<p>
Digging into why turned out to be the most valuable part of the work. Paired significance tests, evidence-removal experiments, and failure-mode audits showed that about a third of the single-type labels don't fit their own Community Note, and that the models make recurring reasoning errors no matter the label: treating the correction itself as "missing context," reading a meme caption as a doctored image, counting copies of one fake quote as independent confirmation, and judging a 2024 post with evidence published in 2025. When I removed all evidence for posts about events after the model's training cutoff, it still claimed strong support for "misleading," citing the lack of evidence as its reason.
</p>
<p>
To test whether the final judgment could run on a fully local, lower-cost model, I also fine-tuned a Qwen3.5-4B verdict agent with QLoRA on a single 16 GB GPU. Its training set of 310 examples was built by keeping targets that multiple models agreed on, drafting the rest with an LLM, validating every draft against the pipeline's gates, and reviewing them in a custom human-review app, with the test set held out entirely. A first, short run reached parity with the original model in the unconstrained variant but not yet in the constrained one; a full-length training run is next.
</p>

## Judging the Judges
<p>
These findings reshaped the project. Agreement with Community Notes labels turned out to be a noisy yardstick, so the thesis now focuses on whether the agentic workflow helps a weak model <em>reason</em> as well as stronger ones. That makes the LLM-as-judge phase central: the judge is deliberately drawn from a different model family than the systems it grades, specifically to catch overconfident or unsupported claims that a same-family judge might be more likely to let slide. It's not just about building agents that seem to work — it's about proving whether they actually do, and being honest about what that proof costs.
</p>

## Status
<p>
This work is ongoing as part of my M.S. thesis at the University of Hawai'i at Mānoa. I'll be updating this page with results and a link to the published thesis as the work progresses.
</p>
