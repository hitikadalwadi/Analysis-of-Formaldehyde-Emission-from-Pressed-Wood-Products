# Analysis-of-Formaldehyde-Emission-from-Pressed-Wood-Products
# Surface Area and VOC Emissions Analysis

A comprehensive Python-based analysis tool for studying formaldehyde (HCHO) and volatile organic compound (VOC) emissions from plywood samples in different arrangements.

## Project Overview

This project analyzes the relationship between surface area exposure and formaldehyde emissions from plywood samples. The study compares emissions between horizontal and vertical arrangements of plywood sheets, providing insights into how stacking configuration affects indoor air quality.

## Key Features

- **Surface Area Calculation**: Automated calculation of exposed surface area for different plywood arrangements
- **Data Processing**: Robust Excel data loading and preprocessing pipeline
- **Statistical Analysis**: Linear regression modeling with comprehensive statistics
- **Visualization**: Professional plots comparing emissions across different configurations
- **Modular Design**: Clean, reusable functions for easy extension and maintenance

## Requirements

```python
pandas>=1.3.0
matplotlib>=3.4.0
numpy>=1.20.0
seaborn>=0.11.0
scikit-learn>=0.24.0
openpyxl>=3.0.0  # For Excel file support
```

## Project Structure

```
voc-analysis/
├── README.md
├── explantory_data_analysis.ipynb          # Main analysis script
├── requirements.txt
├── data/
│   ├── KD_Ply_2V.xlsx      # 2-ply vertical arrangement data
│   ├── KD_horizontal_2.xlsx # 2-ply horizontal arrangement data
│   ├── KD_vertical_3.xlsx   # 3-ply vertical arrangement data
│   ├── KD_horizontal_3.xlsx # 3-ply horizontal arrangement data
│   ├── KD_5_V_ply.xlsx     # 5-ply vertical arrangement data
│   ├── KD_5_H_ply.xlsx     # 5-ply horizontal arrangement data
│   └── KD_MDF_*.xlsx       # MDF comparison data
```

### Quick Start

```python
python explanatory_data_analysis.ipynb
```

The script will prompt you to:
1. Select arrangement type (Vertical or Horizontal)
2. Enter the number of plywood sheets
3. Calculate the exposed surface area

## Data Format

Your Excel files should contain the following columns:
- `Time`: Timestamp of measurement
- `HCHO (mg/m³)`: Formaldehyde concentration
- `PM2.5 (ug/m³)`: Particulate matter concentration
- `TVOC (mg/m³)`: Total volatile organic compounds
- `AQI`: Air Quality Index

## Usage Examples

### Surface Area Calculation

```python
from surface_area import calculate_surface_area

# Interactive calculation
surface_area, arrangement, num_sheets = calculate_surface_area()
```

### Data Analysis

```python
from surface_area import load_and_clean_data, perform_linear_regression

# Load data
data = load_and_clean_data("data/KD_Ply_2V.xlsx", 
                          columns_rename={'HCHO (mg/m³)': 'HCHO_V2'})

# Perform regression analysis
results = perform_linear_regression(data['Minutes'], data['HCHO_V2'], 
                                   "Vertical 2-ply")
```

### Visualization

```python
from surface_area import create_comparison_plot

# Compare multiple datasets
create_comparison_plot(merged_data, 'Minutes', 
                      ['HCHO_H2', 'HCHO_V2'],
                      ['Horizontal 2-ply', 'Vertical 2-ply'],
                      'HCHO Emissions Comparison',
                      'HCHO (mg/m³)')
```

## Analysis Results

### Reference Surface Area Values

| Configuration | Surface Area (m²) |
|---------------|-------------------|
| H_2 (2-ply Horizontal) | 0.07486 |
| V_2 (2-ply Vertical) | 0.19498 |
| H_3 (3-ply Horizontal) | 0.09102 |
| V_3 (3-ply Vertical) | 0.12447 |
| H_5 (5-ply Horizontal) | 0.12370 |
| V_5 (5-ply Vertical) | 0.48745 |

### Maximum HCHO Emissions Observed

| Configuration | Max HCHO (mg/m³) | Temperature |
|---------------|------------------|-------------|
| V2 (2-ply Vertical) | 1.17 | 25°C |
| H2 (2-ply Horizontal) | 0.73 | 25°C |
| H3 (3-ply Horizontal) | 0.75 | 25°C |

## Methodology

### Plywood Specifications
- **Length (L)**: 0.28 m
- **Breadth (B)**: 0.15 m  
- **Height (H)**: 0.019 m

### Surface Area Calculations

**Horizontal Arrangement:**
```
Total Height = N × H
Total SA = (2×L×B) + (2×L×Total_H) + (2×Total_H×B)
Exposed SA = Total SA - (L×B)  // Bottom face contact
```

**Vertical Arrangement:**
```
Total SA = N × ((2×L×B) + (2×L×H) + (2×H×B))
Exposed SA = Total SA - (N×B×H)  // Inter-sheet contact
```

## Statistical Analysis

The analysis includes:
- **Linear Regression**: Time vs HCHO concentration
- **Model Metrics**: R², RMSE, MSE
- **Comparative Analysis**: Different arrangements and materials
- **Trend Analysis**: Emission patterns over time

## Team
- Hitika Dalwadi
- Dr.Kishori Dalwadi


---

**Note**: This analysis is for research purposes. Ensure proper ventilation when working with formaldehyde-emitting materials.
