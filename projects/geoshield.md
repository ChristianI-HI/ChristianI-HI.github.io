---
layout: project
type: project
image: ""
placeholder: true
title: "GeoShield"
date: 2025
published: true
featured: true
labels:
  - Computer Vision
  - Python
  - LLM
  - Privacy
summary: "A two-stage computer-vision pipeline that obscures geo-identifying cues in images to protect people from image-based geolocation."
---

<div class="pf-placeholder">
  <div>
    <span class="pf-placeholder-label">Screenshot placeholder</span>
    Before/after pipeline output — to be added
  </div>
</div>

<hr>

## Introduction
<p>
GeoShield is a privacy-preserving computer-vision tool built over the summer of 2025. The goal: given a photo, automatically obscure the visual cues — street signs, landmarks, distinctive architecture, terrain — that let someone (or an AI model) figure out exactly where it was taken. This kind of image-based geolocation is a real and growing privacy risk, and GeoShield is a step toward making it harder to pull off without the photo's owner's consent.
</p>

## Pipeline
<p>
GeoShield uses a two-stage pipeline. First, <b>GroundedSAM</b> handles object detection and segmentation, identifying the specific regions of an image that carry geo-identifying information. Then, <b>FLUX diffusion inpainting</b> replaces those regions with plausible, non-identifying content — obscuring the location cue while keeping the rest of the image visually coherent, rather than just blurring or blacking out a rectangle.
</p>

## Evaluation
<p>
I evaluated GeoShield on the <b>Doxing Dataset</b> and the <b>FairLocator</b> benchmark, testing whether state-of-the-art geolocation models could still correctly place an image after processing. Across both benchmarks, GeoShield reduced geolocation accuracy and increased median location error, showing that the obscuring pipeline meaningfully degrades a model's ability to pinpoint where a photo was taken.
</p>

## Why This Matters
<p>
Most privacy tools for images focus on metadata (stripping EXIF data) or on obvious identifiers (faces, license plates). GeoShield targets a subtler and increasingly relevant threat: the background of a photo itself, combined with a capable enough vision-language model, can be enough to deanonymize someone's location. As these models get better, tools like this become more important — not just for public figures, but for anyone who posts photos online.
</p>
