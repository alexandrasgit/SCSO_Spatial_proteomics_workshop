# Spatial Proteomics Workshop 2026

Hands-on workshop materials for analysing the spatial architecture of the tumour 
microenvironment using multiplexed tissue imaging data and Python-based tools, 
compiled as a Jupyter Book.

📖 **[Open the Workshop Book](https://farkkilab.github.io/SCSO_2026_Spatial_proteomics_workshop)**

---

## Overview

This workshop introduces computational spatial proteomics analysis — from raw 
multiplexed protein expression to biologically interpretable tissue neighbourhoods. 
All exercises use real high-grade serous ovarian cancer (HGSOC) TMA data.

| Exercise | Topic |
|----------|-------|
| Exercise 1 | Technical foundations of digital pathology |
| Exercise 2 | Biological interpretation & cell phenotyping |
| Exercise 3 | Spatial architecture of the tumour microenvironment |

---

## Tools & Dependencies
```bash
pip install scimap scanpy anndata utag matplotlib scikit-learn
```

| Tool | Purpose |
|------|---------|
| [SCIMAP](https://scimap.xyz) | Spatial single-cell analysis |
| [Scanpy](https://scanpy.readthedocs.io) | Single-cell data handling (AnnData) |
| [UTAG](https://github.com/ElementoLab/utag) | Unsupervised tissue domain discovery |

---

## Data

The dataset used in this workshop is derived from:

> Perez-Villatoro et al. (2025). *Cancer Discovery*. 
> [https://doi.org/10.1158/2159-8290.CD-25-1492](https://doi.org/10.1158/2159-8290.CD-25-1492)

Please cite the original study if you use this data in your own work.

## License

Code and notebooks: [MIT License](LICENSE-CODE)  
Written content and materials: [CC BY 4.0](LICENSE-CONTENT)

---

## Citation

If you use these materials in your teaching or research, please cite:

> Farkkila's Laboratory. (2026). *Spatial Proteomics Workshop 2026*. 
> GitHub. [https://github.com/alexandrasgit/SCSO_Spatial_proteomics_workshop](https://farkkilab.github.io/SCSO_2026_Spatial_proteomics_workshop)
