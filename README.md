# Measuring the Cost of the Spectral Relaxation in Normalized-Cut Image Segmentation

Research project by **Bekay Oryngazy**, completed at **Pioneer Research Institute** (2026) under the mentorship of **Prof. James M. Murphy (Tufts University)**.

- 📄 Paper: [`paper.pdf`](paper.pdf) (September 2026)
- 💻 Experiment notebook: [`spectral_relaxation_experiments.ipynb`](spectral_relaxation_experiments.ipynb)

## Research question

Spectral clustering turns image segmentation into an eigenvalue problem. It is known that this relaxation can be loose. This project asks how much the relaxation costs on an image graph a practitioner would actually build, measured in the units of the normalized-cut objective itself, and which part of the weight function sets that cost.

The project started with a robot. On our FIRST Tech Challenge team, color-based segmentation merged two touching objects of the same color into one region. Separating them is a question about connectivity, not color, which led to graph-based methods.

## Key findings (from the paper)

- On a standard test image, the solver returns a partition with Ncut = 2.36 × 10⁻² while the cheapest single-object partition it passed over scores 3.91 × 10⁻³, a factor of **6.0** in the objective the method is written to minimize.
- The eigenvectors handed to k-means are the cheapest *functions* on the graph, not the cheapest *cuts*. Because Dirichlet energy is quadratic, a gradual ramp spread across a large lattice can undercut the indicator of a genuinely cheap object boundary.
- The bandwidth is the parameter that sets the price of a boundary and decides which kind of function reaches the bottom of the spectrum first.
- Four predictions were registered before the measurements and a fifth after the mechanism was understood. Four of the five failed at least in part, and two earlier conclusions of the project were reversed.

## What the notebook contains

This notebook holds the early experiments of the project (July 2026), written in Python:

| Experiment | What it tests |
|---|---|
| 1. Synthetic validation | k-means vs. spectral clustering on blobs, circles, and moons |
| 2. Real image | Shi–Malik pixel graph and spectral segmentation of the `coins` image |
| 3. Three Laplacians | Unnormalized, symmetric (NJW), and random-walk Laplacians at a borderline bandwidth |
| 4. Bandwidth sensitivity | Adjusted Rand Index as the bandwidth σ varies |
| 5. Runtime scaling | Graph construction vs. eigensolve time as the number of pixels grows |
| 6. Noise robustness | k-means vs. spectral clustering as noise increases |

The graph construction, the three Laplacians, and the eigensolver calls are implemented directly with SciPy sparse matrices (`scipy.sparse.linalg.eigsh`). Later experiments described in the paper are not included in this notebook.

## How to run

Open the notebook in Google Colab or Jupyter and run all cells. Requirements:

```
numpy
scipy
scikit-learn
scikit-image
matplotlib
```

## Tools

Python, NumPy, SciPy (sparse), scikit-learn, scikit-image, Matplotlib, LaTeX.
