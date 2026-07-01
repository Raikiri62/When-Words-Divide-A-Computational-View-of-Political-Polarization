# When Words Divide: A Computational View of Political Polarization

M.Sc. Research Project  
Academic College of Tel Aviv–Yaffo (MTA)

**Author:** Roy Yitzchak  
**Supervisor:** Dr. Ella Rabinovich  
**Grade:** 93

---

## Publication

**Status:** Manuscript currently under preparation for journal submission.

### Citation
*To be added upon publication.*

### DOI
*To be added upon publication.*

---

## Overview

Political polarization is commonly studied through voting behavior, public opinion surveys, and social networks. This research examines polarization from a linguistic perspective by investigating whether ideological communities increasingly assign different meanings and contextual usage patterns to the same political terms.

Using large-scale Reddit discussions spanning approximately fifteen years (2008–2023), the project analyzes how semantic representations of politically relevant vocabulary evolve across Democratic and Republican communities.

---

## Research Focus

The study investigates the dynamics of linguistic polarization in online political discourse over a fifteen-year period, evaluating whether the contextual meanings of political terms used by Democratic and Republican communities have become increasingly divergent over time, and exploring how these differences manifest in practice.

---

## Dataset

### Political Reddit Corpus
* **Target Communities:** Left-leaning (`r/Democrats`, `r/Liberal`) and Right-leaning (`r/Conservative`)
* **Scale:** 
  * 12.4+ million total records (posts and comments combined)
  * 33.5+ million processed sentences (30,177,471 Right-wing, 3,381,569 Left-wing)
* **Temporal Span:** 2008–2023 partitioned into 11 temporal slices to balance resolution with corpus size.

---

## Methodology

### Stage 1 — Political Vocabulary Identification
Rather than relying on manually selected word lists, a data-driven approach isolated politically characteristic vocabulary. Using **Log-Odds Ratio analysis with an Informative Dirichlet Prior**, the combined political corpus was contrasted against a neutral, non-political Reddit baseline corpus (`r/LifeProTips`, `r/Showerthoughts`, `r/relationship_advice`, `r/socialskills`, `r/technology`). After filtering for frequency (≥100 occurrences in both corpora) and removing noise, a final target vocabulary of **851 politically relevant terms** was constructed.

### Stage 2 — Semantic Modeling
Distributional semantic models based on **Word2Vec** (Skip-Gram/CBOW architecture via Gensim) were trained separately for 11 temporal slices. To enable direct ideological comparison within a single joint vector space, tokens were marked with a community-specific suffix (e.g., `patriot_D` and `patriot_R`). This allowed the model to learn distinct contextual representations for the same lexical item. Hyperparameters were tuned against human judgments using the **SimLex-999** benchmark dataset (`vector_size=300`, `window=2`, `sample=6e-5`, `negative=20`, `min_count=100`).

### Stage 3 — Semantic Divergence Measurement
For each target term, semantic divergence between the ideological communities was quantified using a shift score derived from cosine similarity:

$$\text{Shift Score}(w) = 1 - \text{Cosine Similarity}(W_{D}, W_{R})$$

### Stage 4 — Trend Analysis & Era Comparison
* **Fine-Grained Analysis:** The non-parametric **Mann–Kendall trend test** was applied to the time series of shift scores for words with at least 9 valid time points to detect systematic monotonic trends.
* **Coarse-Grained Analysis:** A two-era comparative analysis divided the corpus into an Early period (2009–2018) and a Late period (2018–2023) to measure structural expansion of the semantic gaps.

---

## Key Findings

* **Directional Trend:** Out of 124 words exhibiting statistically significant monotonic temporal trends ($p < 0.05$), **119 words (95.97%)** demonstrated strictly increasing semantic divergence, while only 5 words showed a decreasing trend.
* **Qualitative Archetypes:** Semantic gaps systematically expand over time, manifesting as recurring patterns of asymmetric labeling (e.g., `lefty`, `libs`), identity-based framing vs. negative characterizations (e.g., `MAGA`), event anchoring divergence (e.g., `rioters`, `fraud`), and evaluative shifts (e.g., `woke`, `china`).

---

## Repository Structure

```text
.
├── data/                                 # Raw tokenized/filtered text data splits
├── models/                               # Trained Word2Vec temporal embedding models
├── neighbors/                            # Extracted nearest neighbors of/per target word across models
├── sentence count csvs/                  # Volumetric tracking per subreddit/year
├── shift scores csvs/                    # Output logs of calculated cosine distances
├── simlex results pearson spearman csvs/ # Evaluation logs and hyperparameter grid-search metrics
├── SimLex-999/                           # Standard semantic benchmark dataset
├── words - political terms/              # Final vocabulary construction files (851 isolated terms)
└── thesis.pdf                            # Local copy of the M.Sc. thesis manuscript

```

## Full Report

The complete research report detailing the architectural workflow, mathematical formulations, evaluation metrics, and comprehensive qualitative discussions is included directly in this repository as `thesis.pdf`.

## Future Work

* **Subword Semantics**: Exploring alternative embedding frameworks like FastText to incorporate subword information and improve structural robustness for morphologically complex or rare terms.
* **Global Metrics**: Developing an Aggregate Polarization Index (API) to comprehensively summarize holistic semantic divergence across the entire target vocabulary over distinct epochs.
* **Dataset Expansion**: Extending the timeline beyond 2023 to capture semantic intensification during more recent high-tension geopolitical and macroeconomic cycles.
* **Visual Topography**: Integrating clustering methodologies paired with non-linear dimensionality reduction (t-SNE or UMAP) to visualize the spatial and topological separation of ideological language over time.
* **Contextual Architectures**: Transitioning to modern transformer-based models like Sentence-BERT to move past lexical constraints and evaluate polarization at the sentence and discourse levels.

## Contact

**Roy Yitzchak**  
M.Sc. Computer Science, School of Computer Science  
The Academic College of Tel Aviv-Yaffo, Israel  

**Email**: [Raikiri62@gmail.com](mailto:Raikiri62@gmail.com)
