# PPO Implementation for Founders and Coders: Week 6 Final Project

## 🚀 Overview

This repository contains my final project for the Week 6 workshop, focusing on a deep dive into **Proximal Policy Optimization (PPO)**. This project wasn't just about using a library; it was about understanding the fundamental mechanics of one of the key algorithms driving modern large language models.

The capstone of the workshop was an intense exploration of the math and theory behind PPO, culminating in this implementation.

## 💡 Core Concept: Why PPO?

PPO is a cornerstone algorithm in **Reinforcement Learning from Human Feedback (RLHF)**. This is the training methodology famously used by organizations like OpenAI to align LLMs with human preferences.

The process (which we studied in-depth) generally involves:
1.  **Supervised Fine-Tuning (SFT):** Training a base model on a smaller, high-quality dataset.
2.  **Training a Reward Model:** This is where the "human feedback" comes in. Annotators (e.g., the "expert annotators" OpenAI hires) are shown multiple model outputs and rank them from best to worst. A separate "reward model" is then trained to predict what score a human would give a new, unseen output.
3.  **PPO Training:** The SFT model (now called the "policy") is then trained against the reward model. It's "rewarded" for generating outputs that the reward model *thinks* a human would like. PPO's job is to update the policy to maximize this reward, without straying too far from the original SFT model (this is managed by a KL-divergence penalty).

## 🧠 The Technical Deep Dive: The Math & The Pipeline

[cite_start]A significant portion of this project was spent "getting confused together" (as our slides said [cite: 6]) and then un-confused about the mathematics of PPO. The core of the algorithm lies in its complex objective function.

The entire PPO pipeline we implemented is visualized in this diagram from our workshop materials, which shows how the **Policy Model**, **Reward Model**, **Value Model**, and **SFT Model** all interact.

<img width="1066" height="563" alt="image" src="https://github.com/user-attachments/assets/37f0390e-cee4-4ac7-be8a-96493251c60d" />

*(Diagram based on Week 6 Workshop Slides)*

This pipeline involves:
* **Calculating the Reward:** Combining the score from the **Reward Model** with a **KL penalty** to keep the policy from "over-optimizing" and diverging too far from the original SFT model.
* **Calculating Advantage:** Using Generalized Advantage Estimation (GAE) to determine if an `action` (a generated token) was better or worse than the `value` (the expected reward) for a given `state`.
* **The PPO-Clip Loss:** This is the magic of PPO. It "clips" the objective function to prevent the policy from changing too rapidly in a single update, which is what gives PPO its stability.

This project was a challenging but incredibly rewarding look under the hood of state-of-the-art AI.
