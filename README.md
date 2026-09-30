# 3D Reconstruction & Multi-Sensor Fusion: TLS vs. Close-Range Photogrammetry

A comparative post-processing and sensor fusion study evaluating **Terrestrial Laser Scanning (TLS)** against **Close-Range Digital Photogrammetry (SfM/MVS)** for high-precision 3D digital preservation and geometric analysis.

---

## 📌 Project Overview
The objective of this project is the reconstruction, optimization, and quantitative comparison of 3D models derived from survey datasets of an outdoor monument:
1. **Terrestrial Laser Scanning (FARO Focus):** High-precision geometry from 8 point clouds (>6.6M vertices).
2. **Close-Range Photogrammetry (Canon EOS 550D):** Structure-from-Motion (SfM) processing of 81 high-resolution images.
3. **Hybrid Textured Model:** Combining LiDAR geometric fidelity with high-resolution photogrammetric texture mapping.

---

## 🛠️ Methodological Workflow

### 1. Point Cloud Processing & Meshing (MeshLab)
* **Noise Removal & Preprocessing:** Segmented and filtered unwanted surroundings across 8 raw `.txt` scans (XYZRGB format).
* **Normal Vector Estimation:** Computed surface normals via neighboring point analysis (k-neighbors tuned from 10 to 50) and viewpoint orientation adjustments.
* **Registration & Alignment:** Coarse alignment via manual homologous points, followed by fine registration using the **Iterative Closest Point (ICP)** algorithm (achieved target errors < 4 mm).
* **Surface Reconstruction:** Applied **Poisson Surface Reconstruction** (depth 10) to generate clean, watertight triangular meshes, followed by non-manifold edge and boundary cleaning.

### 2. Digital Photogrammetry Pipeline (Agisoft Metashape Pro)
* **Image Alignment (SfM):** Camera calibration and feature matching on 81 multi-angle images, solving exterior orientation parameters.
* **Dense Cloud Generation:** Computed high-density depth maps with optimized bounding box limits to filter vegetation artifacts.
* **Textured Mesh:** Built high-detail geometry and generated texture atlases using blending weights for photo consistency.

### 3. Sensor Fusion & Hybrid Reconstruction
* Imported the TLS Poisson mesh into Agisoft Metashape.
* Positioned 10 distributed Ground Control Points (GCPs) across the geometry and identified them across multiple photos.
* Executed **Bundle Adjustment** (optimized camera poses, achieving total reprojection error < 0.1 px).
* Projected photogrammetric texture onto the LiDAR-derived geometric surface.

### 4. Quantitative Geometric Inspection (CloudCompare)
* Evaluated geometric discrepancy between the TLS and Photogrammetric meshes using the **Cloud-to-Mesh (C2M)** distance tool.
* Successfully demonstrated model convergence with surface deviations predominantly constrained within **±1–2 cm**.

---

## 💻 Software & Tools
* **Software:** MeshLab, Agisoft Metashape Pro, CloudCompare
* **Data Sources:** FARO Focus TLS scans, Canon EOS 550D DSLR images
