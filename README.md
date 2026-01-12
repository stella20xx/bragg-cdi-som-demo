# Bragg Coherent Diffraction & Gasoline Diffraction with SOM

Unsupervised clustering and segmentation of Bragg coherent diffraction
imaging (CDI) and gasoline / fuel-spray diffraction patterns using
physics-aware Self-Organizing Maps (SOM).

This demo shows how SOM can separate meaningful Bragg peaks, speckle
patterns, and background in coherent X-ray diffraction images, and how
similar ideas extend to fuel-spray/gasoline diffraction data under
different operating conditions.

See the full slide decks in:

- [`docs/bragg_coherent_diffraction_image.pdf`](docs/bragg_coherent_diffraction_image.pdf)
- [`docs/bragg_cdi_and_bragg_gdi.pdf`](docs/bragg_cdi_and_bragg_gdi.pdf)

---

## Problem

- Bragg CDI experiments produce 2D/3D diffraction patterns with
  structured speckle and Bragg peaks that encode nanoscale strain and
  morphology.
- Gasoline / fuel-spray diffraction images add complexity from
  turbulence, multiphase flow, and changing operating conditions.
- Manual masking of peaks vs background and ad-hoc thresholds do not
  scale and are hard to interpret.
- Goal: **cluster and segment diffraction patterns in a label-free,
  physics-aware way**, separating peaks, speckle, and background with
  interpretable clusters.

---

## Data

- **Bragg CDI:**
  - Coherent X-ray diffraction patterns around a Bragg peak.
  - Intensity in reciprocal space encodes strain, shape, and defects.

- **Gasoline / fuel-spray diffraction:**
  - Diffraction images collected under varying conditions (e.g. pressure,
    injection timing), with different scattering signatures.

No hand-drawn masks or supervised labels are assumed.

---

## Method (SOM-based clustering in reciprocal space)

1. **Physics-aware feature extraction**

   Each pixel in a diffraction image is mapped into a feature vector
   including, for example:

   - log-scaled intensity,
   - local contrast and gradient magnitude,
   - distance from Bragg peak / beam center,
   - simple neighborhood statistics (e.g., local variance).

2. **PCA + SOM clustering**

   - PCA reduces the feature dimension while preserving intensity and
     geometric structure.
   - A Self-Organizing Map (SOM) is trained to obtain a small set of
     clusters corresponding to:
     - background / noise,
     - Bragg peak / ring regions,
     - high-intensity speckle or defect-related features.

3. **Cluster interpretation**

   - Clusters are analyzed via their centroid features and spatial
     locations.
   - Radar / feature-profile plots (see PDFs) show how each cluster
     differs in intensity, sharpness, and radial position.
   - For Bragg CDI, clusters can be linked to regions dominated by the
     main Bragg lobe, side lobes, or diffuse scattering.

4. **Cross-condition comparison (GDI)**

   - For gasoline diffraction, SOM codebooks can be reused or
     re-initialized to compare scattering patterns under different
     operating conditions.
   - Differences in cluster occupancy or intensity provide a compact
     descriptor of how spray / cavitation behavior changes.

Key properties:

- **Label-free:** no manual peak masking or region annotation is needed.
- **Physics-aware:** features are defined in terms of intensity and
  reciprocal-space geometry, not arbitrary textures.
- **Interpretable:** each SOM cluster corresponds to a specific
  scattering regime (background, Bragg peak, speckle, diffuse).

---

## Results (see PDFs)

Highlights from the Bragg CDI and gasoline diffraction demos:

- SOM clustering separates background, main Bragg peak, and
  high-intensity speckle regions in coherent diffraction images.
- Cluster maps reveal how different diffraction components are organized
  in reciprocal space.
- For gasoline diffraction, SOM clusters provide a compact way to
  compare scattering patterns across conditions, suggesting features
  that can be used for further modeling or control.

---

## Status

This repository currently serves as a **documentation/demo hub** for the
Bragg CDI and gasoline diffraction SOM pipeline. Code and runnable
notebooks will be added progressively as the framework is cleaned and
released.
