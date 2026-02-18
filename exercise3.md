# Exercise 3: Technical foundations of digital pathology

In this exercise, we transition from viewing images to analyzing the "Social Network of Cells." We will use Scimap for phenotyping and interactions, and UTAG to discover tissue domains.

:::{admonition} Pre-requisites
Ensure you have activated your environment and have the following packages:
pip install scimap utag anndata scanpy
:::

## Loading dataset

Before analyzing space, we must ensure our data table has the "Minimum Viable Columns."

Task: Load your dataset and verify the following fields:

* X, Y coordinates: Usually in ```python adata.obsm['spatial']```.
* Marker Matrix: Expression levels for each protein per cell.
* ROI/ImageID: To separate different tissue samples.

:::{tip}
Question for the group: Thinking about your own research project, what is one spatial hypothesis you’d test? (e.g., "Are T-cells closer to the tumor in Responders vs. Non-responders?")
:::

## Phenotyping with Scimap

We use a "Prior-Knowledge" approach. Instead of unsupervised clustering, we tell the computer what a T-cell looks like based on markers we know.

### Step 1: Rescaling and Gating

Scimap expects data to be rescaled (usually 0 to 1) to make gating consistent across markers.

```python
import scimap as sm
import scanpy as sc

# Load your AnnData object
adata = sc.read_h5ad('lung_cancer_data.h5ad')

# Rescale data
adata = sm.pp.rescale(adata, gate=0.5)
```

### Step 2: Apply Phenotype Workflow

We use a CSV table that defines our cell types (e.g., T-cell = CD3+, CD8-).

```python
# Run phenotyping
adata = sm.tl.phenotype_cells(adata, phenotype_method='all', 
                              label='phenotype')

# Quick Visual QC
sm.pl.spatial_scatter(adata, color='phenotype', s=1)
```

:::{tip}
*Task*: Check your phenotype counts.
*Question*: Which phenotype here is most sensitive to threshold choice, and why?
:::

## Spatial Metrics (interactions & neighborhoods)

Metric A: Cell–Cell Interaction

```python
# Quantify adjacency enrichment (Permutation test)
adata = sm.tl.spatial_interaction(adata, method='radius', radius=30, label='phenotype')

# Visualize significance heatmap
sm.pl.spatial_interaction(adata, threshold=0.01, binary_view=True)
```

Metric B: Neighborhood Composition

```python
# Compute neighborhood proportions
adata = sm.tl.spatial_count(adata, x_coordinate='X_centroid', y_coordinate='Y_centroid', 
                            radius=50, label='phenotype')
```

:::{tip}
Question: If you double the radius from 50μm to 100μm, which biology becomes more visible vs. less specific?
:::

## Tissue Domains with UTAG

While Part 2 looks at individual cell neighbors, UTAG looks at the "Microanatomical Domains" (e.g., Stroma vs. Tumor Nest) by combining phenotypes with a graph-based approach.

```python
import utag

# Run UTAG to find microanatomical domains
# max_dist defines the 'reach' of the adjacency graph
adata = utag.utag(adata, 
                  data_key='X', 
                  cluster_key='phenotype', 
                  max_dist=20, 
                  resolutions=[0.1, 0.3])

# Plot the discovered domains
sc.pl.spatial(adata, color='UTAG_label_res_0.1', spot_size=10)
```
