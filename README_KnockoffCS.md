# KnockoffCS: Knockoff-Guided Compressive Sensing

[![Paper](https://img.shields.io/badge/Paper-arXiv%3A2505.24727-b31b1b.svg)](https://arxiv.org/abs/2505.24727)
[![Status](https://img.shields.io/badge/Code-release%20in%20progress-orange.svg)](https://github.com/xiaochenzhang166/Implementation-of-Knockoff-Guided-Compressive-Sensing)

Official implementation repository for **“Knockoff-Guided Compressive Sensing: A Statistical Machine Learning Framework for Support-Assured Signal Recovery”** by **Xiaochen Zhang and Haoyi Xiong**.

**[Paper](https://arxiv.org/abs/2505.24727) · [PDF](https://arxiv.org/pdf/2505.24727)**

## Overview

Compressive sensing aims to recover a high-dimensional sparse signal from a limited number of noisy linear measurements. In addition to estimating signal values, accurately identifying the nonzero components—the **support**—is critical. Standard reconstruction methods such as LASSO and orthogonal matching pursuit (OMP) do not explicitly control the false discovery rate (FDR) of the recovered support.

**KnockoffCS** integrates statistical knockoff-based selection into the compressive sensing pipeline. It separates support identification from coefficient estimation: knockoff variables provide negative controls for selecting signal components at a target FDR level, after which the selected coefficients are estimated using least squares or ridge regression. The paper investigates theoretical recovery and FDR properties under its stated assumptions and evaluates the method on synthetic and real-world data.

## Method

Consider the noisy measurement model

$$
\mathbf y = \mathbf A\mathbf x + \mathbf w,
$$

where $\mathbf A$ is the measurement matrix, $\mathbf x$ is the unknown sparse signal, and $\mathbf w$ is measurement noise. Given $\mathbf y$, $\mathbf A$, and a target FDR level $q$, the proposed framework follows three stages:

1. **Knockoff construction.** Construct a knockoff measurement matrix $\widetilde{\mathbf A}$ from the original measurement matrix, designed to preserve relevant correlation structure.
2. **FDR-guided support selection.** Compare the original and knockoff features using the importance statistic

   $$
   W_j = |(\mathbf A^\top \mathbf y)_j| - |(\widetilde{\mathbf A}^\top \mathbf y)_j|.
   $$

   Apply the paper's data-dependent thresholding procedure at the target level $q$ to estimate the support $\widehat{S}$.
3. **Signal reconstruction.** Estimate coefficients on $\widehat{S}$ using least squares or ridge regression and set the remaining coefficients to zero.

See **Section 3 and Algorithm 1** of the [paper](https://arxiv.org/html/2505.24727) for the full construction, thresholding procedure, and implementation details. The theoretical claims are subject to the assumptions and conditions discussed in the paper; they should not be interpreted as unconditional FDR guarantees for arbitrary underdetermined measurement matrices.

## Experimental Evaluation

The paper evaluates KnockoffCS against conventional reconstruction approaches, including LASSO and OMP-guided compressive sensing.

- **Synthetic experiments:** Examine support recovery (including F1-score, FDR, and statistical power) and signal reconstruction errors across different measurement and noise settings. The paper reports up to **3.9× higher F1-score** than baseline methods in its evaluated simulation settings.
- **Real-world experiments:** Evaluate recovered representations on downstream regression and classification tasks, comparing reconstruction approaches as well as compressed and original uncompressed representations.

These are results reported in the paper; consult the paper for experimental configurations, individual comparisons, and limitations.

## Repository and Reproducibility

This repository is intended to provide the implementation and experiment scripts accompanying the paper, including synthetic experiments and real-data evaluations.

**Release status:** Code and documentation are being organized. The installation instructions, verified entry points, and dataset preparation steps will be added as the corresponding files become available. Please do not treat the paper's algorithm description alone as a verified, ready-to-run software interface.

<!-- Once files are finalized, replace this section with a verified directory tree,
     dependency installation command, dataset download/preprocessing instructions,
     and exact commands for each experiment and figure. -->

## Citation

If you find this work useful, please cite:

```bibtex
@misc{zhang2025knockoffguidedcompressivesensing,
  title={Knockoff-Guided Compressive Sensing: A Statistical Machine Learning Framework for Support-Assured Signal Recovery},
  author={Xiaochen Zhang and Haoyi Xiong},
  year={2025},
  eprint={2505.24727},
  archivePrefix={arXiv},
  primaryClass={stat.ML},
  url={https://arxiv.org/abs/2505.24727}
}
```

## Questions

For questions about the methodology or the accompanying experiments, please open a GitHub issue.
