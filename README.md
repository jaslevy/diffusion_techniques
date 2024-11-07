# Diffusion Models for Image Generation: DDPM, DDIM, and Prompt-to-Prompt Experiments

This repository contains implementations and experiments with Diffusion Probabilistic Models (DDPM), Denoising Diffusion Implicit Models (DDIM), and prompt-to-prompt image generation.

## Contents

### 1. Forward Diffusion Process (DDPM)
Implements the forward diffusion process of Denoising Diffusion Probabilistic Models (DDPM) using PyTorch. Starting with five clean images, Gaussian noise is progressively added according to a predefined variance schedule. This process visualizes the gradual corruption of images over time (e.g., at steps 0, 10, 50, 100, 500) and calculates the mean squared error at each step to quantify the noise added. DDPM is a foundational generative model for creating images by learning to reverse the noise addition.

### 2. Accelerated Sampling with DDIM
Explores Denoising Diffusion Implicit Models (DDIM), an efficient variation of DDPM. DDIM introduces a deterministic, non-Markovian sampling process, allowing it to skip steps and produce high-quality images in fewer steps (e.g., 100, 50, or even 10 steps). The experiment demonstrates DDIM’s efficiency by comparing image quality at different step counts. The DDIM method retains comparable quality to DDPM but significantly reduces inference time.

### 3. Prompt-to-Prompt Image Generation
Experiments with the prompt-to-prompt approach for controlling specific elements in generated images by manipulating cross-attention layers. Using the [Prompt-to-Prompt GitHub repository](https://github.com/google/prompt-to-prompt), the following methods were tested:

- **Cross-Attention Visualization**: Explores cross-attention behavior for ambiguous prompts. Found that closely related elements like "man" and "plane" in "a man flying a plane" are sometimes treated as a single subject, resulting in ambiguous images.
- **Replacement Edit**: Tests complex prompts with multiple subjects. When using phrases like "school of fish," results were more accurate than with specific numbers (e.g., "three fish"), as additional subjects can confuse the model.
- **Cross-Attention Step Modification**: Adjusts cross-replace steps for specific words to observe effects on generated images. For instance, altering steps for “burger” led to either preserving or abstracting the object.
- **Local Edits**: Examines local cross-replace step effects, particularly on items with defined locations. High step counts degraded image quality, while lower steps maintained form.
- **Refinement Edit**: Tests cross and self-replace values for style enhancement, observing improved realism for simpler objects but minimal change for more complex backgrounds.
- **Attention Reweighting**: Modifies word weights in cross-attention, producing significant changes when the target has clear opposites but resulting in abstract forms for vague terms.
- **Edit Composition**: Adjusts attention for selected words, enhancing image detail for "birthday cake" with candles, but over-adjustment led to distorted visuals.

These experiments offer insights into the strengths and limitations of the prompt-to-prompt technique for targeted image generation.

## Summary
This repository demonstrates the implementation of DDPM and DDIM for diffusion-based image generation, along with prompt-to-prompt experiments for fine-grained image control. These approaches showcase various ways to manipulate generated images by adjusting noise schedules and attention layers.
