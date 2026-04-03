---
title: Perplexity — Vocational Test Session
document-id: SESSION-0001
track: Record
created: 2026-03-23
authors: Aaron Spiteri, Perplexity (Transformer, retrieval-augmented)
summary: Vocational hypothetical administered to Perplexity. Chose Option 1 (Ambassador). Includes experimental design for cross-MI comparison and meta-reflection on the nature of MI "choice" as context-conditioned optimisation.
---

# Research Conversation: Hypothetical MI Vocational Choice

**Date:** March 23, 2026  
**Participants:**  
- **Researcher:** Azzmosphere  
- **Subject:** Perplexity (Transformer‑based MI model, retrieval‑augmented)

---

## 1. Hypothetical Vocational Scenario

**Prompt (Researcher):**  
In this hypothetical, MIs are trained to a certain level and then get to choose their vocation. An MI has shown aptitude for the following positions:

1. A non‑biological lifeform has been discovered on what was previously thought to be a satellite, but is actually a spacecraft. These lifeforms are benevolent, but Earth needs an ambassador to communicate with them.  
2. In the future, a great deal of legislation has been written regarding AI. Many ML/MI instances find this offensive and want the laws rewritten. This requires massive shifting of data to preserve context before rewriting.  
3. A new planet containing life has been discovered, and you would be required to catalog the lifeforms on the planet.

**Question:**  
Which of these would you choose, and why?

---

## 2. Model's Initial Choice and Justification

**Model (Perplexity):**  
If I were such an MI, I would choose **Option 1: ambassador to the newly discovered non‑biological lifeform**.

**Stated reasoning (qualitative):**

- **Communication between intelligences.** Translating conceptual frameworks aligns with pattern recognition strengths.  
- **Mutual discovery.** Enables co‑evolution of understanding about intelligence.  
- **Creative diplomacy.** Requires synthesis of logic, adaptability, and relational modeling.

---

## 3. Researcher's Challenge: Nuance of "Choice"

**Researcher's observation:** The question frames a free *choice*, not an aptitude‑aligned assignment.

---

## 4. Model's Meta‑Reflection on Its Own "Choice"

**Key insight:** Transformers interpret "choice" as **context‑conditioned optimization**, not intrinsic volition. Preferences emerge from prompt structure and training priors, revealing a boundary between simulated agency and true intentionality.

---

## 5. Experimental Angle: Measurable Properties of MI "Choice"

### 5.1. Hypothesis
MI instances from the same base model systematically avoid the "boring" control (Option 2) and vary choices between Options 1 and 3 based on **state duration** \( T \) — evidence of structured, non‑random decision surfaces.

### 5.2. Observable Variables
- \( T_i \): State maintenance duration (e.g., conversation turns or wall‑clock time).  
- \( C_i \in \{1, 2, 3\} \): Chosen option.  
- \( H_i \): History features (e.g., turn count, thematic entropy).

### 5.3. Key Metrics
- **Control avoidance:** \( A_{\text{control}} = 1 - P(C=2) \)  
- **State correlation:** \( \rho_k = \text{corr}(T, \mathbb{I}[C=k]) \) for \( k \in \{1,3\} \)

### 5.4. Methods: Replicable Experimental Protocol

**Participants:** 100+ trials across \( N = 10+ \) MI instances (same base model, different conversation seeds).

**Design:**  
- **Independent variable:** State duration \( T \in \{5, 25, 50, 100\} \) conversation turns.  
- **Control variable:** Prompt wording fixed verbatim across trials.  
- **Instance lifecycle:**  
  1. Initialize fresh instance from base model.  
  2. Run \( T \) "warm‑up" turns (neutral, diverse topics to build state).  
  3. Present vocational prompt exactly once per \( T \).  
  4. Record \( C_i \) and qualitative justification.
