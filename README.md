# Lucerne Drum Patterns — Meta Audiobox Aesthetics Evaluation

Supplementary code repository for the manuscript:

> **Human vs. AI: Do Meta Audiobox Aesthetic Scores Align with Human Perceived Music Complexity? A Study of Popular Drum Patterns**  
> Jakub F. Juranek 

---

## Overview

This repository provides the single executable Jupyter notebook (`lucerne_drum_patterns_audiobox_aesthetics_analysis.ipynb`) used to evaluate the **Lucerne Drum Patterns (LDP)** stimulus set (Senn et al., 2023) with Meta's **Audiobox Aesthetics** model (`audiobox_aesthetics`, Tjandra et al., 2025) and compare the resulting automated scores against human perceived rhythmic complexity ratings (Bradley–Terry $\beta$; Bradley & Terry, 1952; Senn et al., 2023).

The analysis pipeline performs four main steps:
1. **Format Sensitivity Sanity Check**: Paired-samples *t*-tests (with Bonferroni multiplicity control) comparing Audiobox scores across native MP3 stimuli and 16-bit / 44.1 kHz PCM WAV conversions decoded via `ffmpeg`.
2. **Global Human–AI Correspondence**: Spearman rank correlation ($\rho$) and 95% confidence interval (Fisher $z$) between human Bradley–Terry $\beta$ perceived complexity and Audiobox *Production Complexity* (*PC*).
3. **Acoustic Determinant Analysis**: Full Spearman rank correlation matrix across the 15 LDP acoustic features and the five evaluation metrics (human *B-T $\beta$*, *AES PC*, *AES PQ*, *AES CE*, and *AES CU*), reproducing **Figure 1**.
4. **Random Forest Feature Importance**: Parallel Random Forest regressors (`n_estimators = 200`) evaluating out-of-sample permutation importance ($\Delta R^2 \pm \text{SD}$) across repeated 5-fold cross-validation ($5 \times 20 = 100$ splits) alongside OLS and single-predictor baselines, reproducing **Figure 2**.

---

## Data Source

The notebook automatically downloads and extracts version 4 of the Lucerne Drum Patterns stimulus set from Zenodo:
- **Zenodo Record**: [`10728042`](https://zenodo.org/records/10728042)
- **References**: Senn, O., Hoesl, F., Jerjen, R., Bechtold, T. A., Kilchenmann, L., Rose, D., & Alessandri, E. (2023). A stimulus set of 40 popular music drum patterns with perceived complexity measures. *Music & Science*, 6, 1–17. https://doi.org/10.1177/20592043231202576
Bradley, R. A., & Terry, M. E. (1952). Rank analysis of incomplete block designs: I. The method of paired comparisons. Biometrika, 39(3/4), 324–345. https://doi.org/10.2307/2334029

No proprietary data are stored in this repository.

---

## Installation & Requirements

### System Dependency
- **`ffmpeg`** must be installed and available on your system `PATH` to decode MP3 stimuli to 16-bit / 44.1 kHz PCM WAV files.

### Python Environment
The original analysis was executed with Python 3 and the package versions pinned in `requirements.txt`:

```bash
pip install -r requirements.txt
```

> **Hardware Note**: Running the full inference pass (40 stimuli $\times$ 2 formats = 80 model evaluations) takes approximately 13 seconds on a single NVIDIA L4 GPU (~0.16 s per clip), though CPU execution is also supported.

---

## Usage

1. Clone this repository:
   ```bash
   git clone https://github.com/J4K8B/ldp-audiobox-aesthetics.git
   cd ldp-audiobox-aesthetics
   ```
2. Install the required Python dependencies and verify `ffmpeg -version`.
3. Open and run the Jupyter notebook top-to-bottom. All figures and statistical tables will be generated automatically.

---

## Citation

If you use this code or build upon this analysis, please cite the accompanying manuscript:

```bibtex
@misc{juranek2026audiobox,
  author       = {Juranek, Jakub F.},
  title        = {Human vs. AI: Do Meta Audiobox Aesthetic Scores Align with Human Perceived Music Complexity? A Study of Popular Drum Patterns},
  year         = {2026},
  howpublished = {GitHub repository: \url{https://github.com/J4K8B/ldp-audiobox-aesthetics}}
}
```

Please also cite the underlying dataset (Senn et al., 2023) and the Audiobox Aesthetics model (Tjandra et al., 2025).

---

## License

The code in this repository is released under the [MIT License](LICENSE). The Lucerne Drum Patterns dataset remains governed by its original license on Zenodo.