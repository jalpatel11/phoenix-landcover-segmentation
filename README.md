# 🛰️ Land Use Land Cover Segmentation in Central Phoenix (2022–2025)

This project performs **land use and land cover (LULC) segmentation** on satellite imagery from **Sentinel-2** for the **Central Phoenix** region between **2022 and 2025**, using the **Dynamic World V1** dataset for labels. The objective is to classify satellite pixels into meaningful categories such as urban areas, vegetation, water, and more using a U-Net deep learning model.

---

## 📍 Region of Interest

- **Location**: Central Phoenix, Arizona, USA  
- **Time Period**: January 2022 – January 2025  
- **Area**: Exported using Google Earth Engine with a resolution of 10 meters  

---

## 🗂️ Dataset

### 🔷 Input Imagery

- **Source**: Sentinel-2 (ESA, Copernicus)  
- **Bands Used**: B2 (Blue), B3 (Green), B4 (Red), B8 (NIR)  
- **Preprocessing**:
  - Normalized reflectance (divided by 10,000)
  - NaN values filled with 0
  - Clipped to range [0, 1]

### 🔶 Labels

- **Source**: Google Dynamic World V1  
- **Classes (9 total)**:
  1. Water  
  2. Trees  
  3. Grass  
  4. Flooded Vegetation  
  5. Crops  
  6. Shrub & Scrub  
  7. Built Area  
  8. Bare Ground  
  9. Snow & Ice  
- **Label Type**: Mode composite (most frequent class from 2022–2025)

---

## 🧠 Model Architecture

A custom **U-Net** model built using TensorFlow and Keras:
- 3 levels of downsampling and upsampling  
- Encoder-decoder skip connections  
- Final softmax activation for 9-class pixel-wise classification  

---

## 🏋️ Training Details

- **Input Size**: 256×256×4 image patches  
- **Loss**: Categorical Crossentropy  
- **Optimizer**: Adam  
- **Metrics**: Accuracy  
- **Callbacks**:
  - ModelCheckpoint
  - ReduceLROnPlateau
  - EarlyStopping  

---

## 📊 Results

✅ **Pixel Accuracy**: 95.95%  
✅ **Weighted F1 Score**: 95.50%  
✅ **Mean IoU**: 92.79%

⚠️ Some classes like *Crops* or *Flooded Vegetation* are underrepresented, which may reduce per-class performance.

---

## 📈 Visualizations

- Patch-level predictions vs ground truth  
- Full-size prediction map (stitched from patch-wise inference)  
- Confusion matrix and classification report  

---

## 📄 Report

You can view the full research report here: [📄 report.pdf](./report.pdf)

---

## 🚀 Getting Started

Follow these steps to set up and run the project on your local machine.

### 1. Clone the Repository

```bash
git clone https://github.com/jalpatel11/phoenix-landcover-segmentation.git
cd phoenix-landcover-segmentation
```

### 2. Create a Virtual Environment

```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Launch the Jupyter Notebook

```bash
jupyter notebook main.ipynb
```

This will open the notebook in your browser. You can run each section to reproduce the full workflow, from data loading to final evaluation and visualization.

---

## 📦 Dependencies

The project uses the following Python libraries:

- numpy
- rasterio
- matplotlib
- scikit-image
- scikit-learn
- seaborn
- tensorflow
- jupyter

Install them all via:

```bash
pip install -r requirements.txt
```

---

## 🔮 Future Work

- Extend to more Sentinel-2 bands or higher resolution imagery
- Experiment with advanced architectures like DeepLabV3+ or FPN
- Introduce class rebalancing or focal loss to handle imbalance
- Integrate time-series change detection
- Build an interactive dashboard for urban planning insights
