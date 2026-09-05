# Probabilistic Graphical Models — Cheat Sheet

## How these topics connect

1. **Probability** — foundation: how likely is something?
2. **Bayes’ Rule** — update a belief when new evidence appears
3. **Naive Bayes** — simple probabilistic classifier
4. **Bayes Nets** — graph of dependencies; compact joint distribution
5. **Inference** — answer queries like \(P(X \mid E)\) in that structure
6. **HMMs** — Bayes-style sequential model with hidden states over time
7. **DTW** — sequence alignment / distance (not a probabilistic model)

---

## Big picture

- Probabilistic models help an AI **reason under uncertainty**.
- Instead of true/false only, you track **how likely** different world states are.
- A **belief state** is a probability distribution over possible states.

---

## Probability

| Idea | Meaning |
|---|---|
| **Joint** \(P(A,B)\) | Probability of multiple events together |
| **Conditional** \(P(A \mid B)\) | Probability of \(A\) given \(B\) |
| **Chain rule** | \(P(A,B) = P(A \mid B)\,P(B)\) |

**Bayes’ Rule** — update beliefs when new evidence appears:

\[
P(H \mid E) = \frac{P(E \mid H)\,P(H)}{P(E)}
\]

| Term | Role |
|---|---|
| **Prior** \(P(H)\) | Belief before evidence |
| **Likelihood** \(P(E \mid H)\) | How expected the evidence is under hypothesis \(H\) |
| **Posterior** \(P(H \mid E)\) | Updated belief after evidence |

**Watch for**

- Mixing up \(P(A \mid B)\) with \(P(B \mid A)\)
- Forgetting that probabilities must sum to 1 over all outcomes

---

## Naive Bayes

A classifier based on Bayes’ Rule. The **naive** assumption: features are **conditionally independent given the class**.

\[
P(C \mid x_1,\ldots,x_n) \propto P(C) \prod_i P(x_i \mid C)
\]

- Compute a class score from prior + feature evidence
- Choose the class with the highest posterior

**Why it works surprisingly well:** simple, fast, and often effective even when independence is not perfectly true.

**Common uses:** spam detection, text classification

**Watch for**

- Zero-probability issues for unseen features (need smoothing)
- The independence assumption is **given the class**, not “features are independent in general”

---

## Bayes Nets

A **directed graph** of random variables:

- **Nodes** = variables
- **Edges** = direct conditional dependencies
- Each node has a **CPT** (conditional probability table) given its parents

**Main benefit:** compactly represents a joint distribution by exploiting conditional independence, instead of storing one giant full-joint table.

\[
P(X_1,\ldots,X_n) = \prod_i P(X_i \mid \mathrm{Parents}(X_i))
\]

---

## Inference in Bayes Nets

**Goal:** answer queries like “what is \(P(X \mid E)\)?”

| Role | Meaning |
|---|---|
| **Evidence** \(E\) | Observed variables |
| **Query** \(X\) | What you want to know |
| **Hidden** | Unobserved variables you may need to sum out |

**Typical steps**

1. Combine the relevant local probabilities
2. **Marginalize** (sum out) hidden variables
3. **Normalize** if needed

**Watch for**

- Forgetting to condition on evidence
- Forgetting to sum over hidden variables
- Confusing graph structure with the actual numeric probabilities

---

## Hidden Markov Models (HMMs)

Used for **sequences** where the true state is hidden but produces observable outputs.

| Piece | Meaning |
|---|---|
| **Initial** \(P(s_1)\) | Starting-state probabilities |
| **Transition** \(P(s_t \mid s_{t-1})\) | How the hidden state evolves |
| **Emission** \(P(o_t \mid s_t)\) | What the current state “says” / outputs |

**Independence assumptions**

- State at time \(t\) depends only on the state at \(t-1\)
- Observation at time \(t\) depends only on the current hidden state

**Typical tasks**

| Task | Question |
|---|---|
| **Likelihood** | How probable is this observation sequence? |
| **Decoding** | What hidden-state sequence is most likely? (e.g. Viterbi) |
| **Learning** | Estimate model parameters from data |

**Course example:** part-of-speech tagging (words = observations, tags = hidden states)

**Watch for**

- Mixing **transition** vs **emission** probabilities
- Forgetting that observations are visible but states are hidden

---

## Dynamic Time Warping (DTW)

Compares two time series that may be **misaligned in time**. Similar patterns can happen faster or slower in different sequences.

- Instead of matching point 1 to point 1 rigidly, DTW finds the **best alignment path**
- Stretch / compress time locally to align similar shapes

**Useful for:** speech, gesture, sensor, and other sequence pattern matching

**Watch for**

- DTW is an **alignment / distance method**, not a probabilistic model like Bayes Nets or HMMs
- “Best alignment” does **not** mean “same length at the same positions”

---

## Fast memory hooks

| Topic | Hook |
|---|---|
| Probability | “How likely?” |
| Bayes’ Rule | “Update belief with evidence” |
| Naive Bayes | “Classify with independent features (given the class)” |
| Bayes Net | “Graph of dependencies” |
| Inference | “Compute query from evidence” |
| HMM | “Hidden states over time” |
| DTW | “Align sequences that run at different speeds” |
