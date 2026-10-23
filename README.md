# MSC-scaffold-RD-ML

Coupled reaction–diffusion and machine-learning pipeline for predicting
mesenchymal stem cell (MSC) lineage commitment (osteogenic, chondrogenic,
adipogenic) from scaffold design parameters: pore radius, stiffness and
oxygen tension.

Everything runs from a single notebook, `MSC_scaffold_pipeline.ipynb`, with
no manual steps between stages:

| Stage | What it does | Output |
|---|---|---|
| Reaction–diffusion solver | Dimensionless steady-state O₂ transport in a pore with Michaelis–Menten consumption; gives the core-depletion index δ as a function of the Damköhler number. | `figures/fig1_rd_profiles.*` |
| Literature dataset | 67 scaffold conditions curated from 18 published studies (protocol in `results/curation_protocol.txt`; estimated moduli are flagged). | in-notebook table |
| Feature engineering | Physics-based features: δ (transport) and Σ (curvature–stiffness stimulus). | `results/dataset_features.csv`, `figures/fig2_scatter.*` |
| Gaussian-process classifier | Lineage prediction with feature ablation. | `results/gp_results.json`, `figures/fig_gp_performance.*` |
| Design maps | Predicted lineage across the pore-radius / stiffness / O₂ design space. | `figures/fig3_design_maps.*` |
| Sensitivity analysis | Sobol indices for the model inputs. | `results/sobol_results.json`, `figures/fig4_sobol.*` |

## Running

```bash
pip install numpy scipy pandas scikit-learn matplotlib seaborn SALib jupyter
jupyter notebook MSC_scaffold_pipeline.ipynb
```

Run the cells in order; Cell 0 defines constants used by every later stage.
To extend the dataset, append rows to `RAW_DATA` in Cell 2 following the
schema `(paper_id, Rp_um, E_kPa, O2_pct, polymer, label, E_estimated)`.

## Status

Exploratory project; results are preliminary and unpublished.

## Author

Marco Fronzi, School of Physics, The University of Sydney — marco.fronzi@sydney.edu.au
