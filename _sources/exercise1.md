# Exercise 1: Technical foundations of digital pathology

In this exercise, we use **Avivator**, a lightweight, web-based visualizer for high-bit-depth OME-TIFF images. While we are using a web tool, the principles of contrast adjustment, bit depth, and spatial metadata apply to all major platforms like **Napari**, **QuPath**, and **Fiji**.

## Getting Started

1. **Launch the Viewer:** [Click here to open the Lung Cancer (LuCa) 7-color dataset in Avivator](https://avivator.gehlenborglab.org/?image_url=https://viv-demo.storage.googleapis.com/LuCa-7color_3x3component_data.ome.tif).
2. **Explore the Interface:** On the right-hand side, you will see the **Channel Controller**.

---

## Understanding multiplexed channels

Click on any channel name to expand the full list.

:::{admonition} TASK: Count the available channels and look at the metadata (wavelengths/names).
**Question:** How many channels are present, and what is the relationship between the wavelength (nm) and the assigned color?
:::

:::{dropdown} Click for Answer
There are **7 channels** (including DAPI). Wavelengths usually correspond to the emission spectra of the fluorophores used (e.g., 465nm for Blue/DAPI).
:::

---

## Intensity ranges & bit depth

Spatial proteomics data often has a much wider dynamic range than standard photos.

1. Toggle all channels **OFF** except for one.
2. Slide the **Min/Max** bars in the channel controller.
3. Open the "three-dot" menu next to the channel and select **"Full"**.

:::{admonition} TASK: Bit depth discovery
:class: tip
Based on the maximum value visible on the slider when set to "Full," what is the **bit depth** of this image?
*Hint: $2^8 = 256$, $2^{16} = 65,536$.*
:::

---

## Spatial metadata (Pixels vs. Microns)

Visualization is only useful if it is spatially accurate.

* **Hover & Inspect:** Move your mouse over a bright cell. Observe the intensity value changing in the UI.
* **Zoom to Pixel Level:** Scroll in until you see individual square pixels. Look at the **Scale Bar** at the bottom.

**Question:** What is the physical size of one pixel in microns ($\mu m$)?

:::{admonition} TASK: Why does pixel size matter?
:class: tip
How would an incorrect pixel-to-micron scale affect your calculation of **cell density** or **cell-to-cell distance** in a spatial neighborhood analysis?
:::

---

## Composites & data integrity

1. Activate these 6 channels: **PDL1, CD8, FoxP3, CD68, CK, and DAPI**.
2. Customize the colors to create a high-contrast "Snapshot."
3. **Right-click → Save As** to take a snapshot of a Region of Interest (ROI).

:::{warning} Critical Thinking: "Snapshot" trap
Your colleague saves a snapshot from Avivator (a `.png` or `.jpg`) and uses it for downstream intensity quantification instead of using a cropping tool like QuPath.

**Are these results equivalent to using the raw OME-TIFF? Why or why not?**
:::

:::{dropdown} Click for the Explanation
**No.** Snapshots are typically **8-bit RGB** (0-255). They compress the raw 16-bit signal and "bake in" your visual contrast adjustments. For science, you must always quantify the **raw 16-bit OME-TIFF** values to maintain linearity and dynamic range.
:::
