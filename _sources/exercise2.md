# Exercise 2: Biological interpretation & cell phenotyping

Now that you’ve mastered the technical aspects of image viewing, we will apply these skills to a real-world clinical sample: a **Lung Cancer specimen** imaged via Cyclic Immunofluorescence (t-CyCIF).

## From pixels to segments

Before we can count cells, a computer must "segment" them—drawing a digital boundary around every individual cell based on nuclear (DAPI) and/or membrane/cytoplasmic markers.

:::{admonition} TASK: Open the [LUNG-3 Data Processing Tour](https://www.cycif.org/data/du-lin-rashid-nat-protoc-2019/osd-LUNG_3_DATA#s=0#w=0#g=0#m=-1#a=-100_-100#v=1_0.6508_0.5#o=-100_-100_1_1#p=Q).
:class: tip

1. Navigate to the **"Cell Segmentation"** page of the tour.
2. Toggle the **Tumor Cells** and **Immune Cells** data labels in the viewer.
3. Observe the "Masks" (the colored outlines representing individual cells).

**Questions:**

* **Morphology vs. Mask:** How does the segmentation algorithm handle a large, sprawling Tumor cell versus a small, round Lymphocyte?
* **Identify Errors:** Can you find an area where two cells are merged into one mask (**Under-segmentation**) or one cell is split into two (**Over-segmentation**)?
* **Downstream Bias:** If the computer misses the cell boundary and captures signal from a neighbor, how will that affect your "Mean Intensity" data?
:::

---

## Defining phenotypes

A **Cell Phenotype** is the observable identity of a cell, defined by the specific combination of proteins it expresses.

:::{admonition} TASK: 
:class: tip
Switch to the [LUNG-3 Histology & Phenotype Viewer](https://www.cycif.org/data/du-lin-rashid-nat-protoc-2019/osd-LUNG_3#s=0#w=0#g=0#m=-1#a=-100_-100#v=1_0.6508_0.5#o=-100_-100_1_1#p=Q).
:::

### Morphology & Lineage

Spatial proteomics allows us to distinguish cells not just by *what* they express, but by *how they look*.

:::{admonition} TASK:
:class: tip

* **The Ratio Challenge:** Compare a **Keratin+** epithelial cell to a **CD3+** lymphocyte.
* **Question:** Which cell type typically has a higher cytoplasm-to-nucleus ratio?
* **Estimation:** Using the scale-bar in the viewer, what is the approximate diameter (in $\mu m$) of a typical lymphocyte in this tissue?
:::

### Subcellular localization

Knowing *where* a protein is supposed to be helps us identify real signal from "noise."

| Category | Definition | Example from this dataset |
| :--- | :--- | :--- |
| **Nuclear** | Stains the DNA or proteins inside the nucleus. | DNA (Hoechst/DAPI) |
| **Cytoplasmic** | Stains the main body/cytoskeleton of the cell. | Keratin, $\alpha$-SMA |
| **Membranous** | Stains the outer boundary (the "skin") of the cell. | CD3, CD8, PD-L1 |

:::{admonition} TASK:
:class: tip
Identify one marker in this image that is purely **Nuclear** and one that is purely **Membranous**.
:::

---

## Lineage vs. functional markers

* **Lineage Markers:** Define the cell "type" (e.g., "I am a T-cell").
* **Functional Markers:** Define the cell "state" (e.g., "I am currently dividing").

:::{admonition} TASK:
:class: tip
Locate **Ki67** in the viewer. Since it only appears when a cell is in the active phases of the cell cycle, is it a Lineage or Functional marker? Why?
:::

---

## The "Real World" Challenge: Signal Aggregation

Navigate to the **"Cytotoxic T-cells"** tab and zoom in on a dense cluster of CD8/CD3 positive cells.

:::{admonition} BONUS: Segmentation headache
:class: danger
When cells are tightly packed or "aggregated," their signals often overlap.

1. **The Border Problem:** If two T-cells are touching, how does the computer decide where one membrane ends and the other begins?
2. **The "False Positive" Trap:** If a CD8 signal "bleeds" into the mask of a neighboring cell that doesn't actually express CD8, how might this lead to errors in your final cell counts?
:::

---

## Summary of Findings

Before finishing, reflect on **Intensity Thresholding**:
If you set your "Min" intensity too high (as practiced in Exercise 1), would you lose the "weakly positive" PD-L1 cells? How does this impact our understanding of tumor microenvironment?
