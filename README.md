# SiPM02 Waveform Processing and Analysis

## Overview

This repository contains two Jupyter notebooks for processing and analyzing Silicon Photomultiplier (SiPM) waveform data acquired from an oscilloscope.

The workflow consists of:

1. Reading raw oscilloscope waveform files (`.csv` / `.Wfm.csv`)
2. Converting the data into structured NumPy waveform arrays
3. Performing pulse and charge analysis
4. Extracting:

   * Pulse charge
   * Peak timing
   * Single Photoelectron (SPE) response
   * Excess Charge Factor (ECF)
   * Gain-related quantities
5. Generating diagnostic plots and finger plots

The notebooks are designed for SiPM characterization studies, including low-light and cryogenic detector measurements.

---

# Repository Structure

```text
.
├── SIPM02_readfile.ipynb          # Reads oscilloscope waveform files
├── SiPM02_Analysis_fixed.ipynb    # Pulse processing and SiPM analysis
├── SiPM02/                        # Folder containing raw waveform files
├── waveforms/                     # Saved processed waveform arrays (.npy)
├── processed_data/                # Optional processed outputs
└── Pulse_Analysis_CH2.csv         # Example comparison/summary file
```

---

# 1. SIPM02_readfile.ipynb

## Purpose

This notebook reads oscilloscope waveform files and converts them into NumPy arrays for efficient downstream analysis.

It supports waveform files saved from oscilloscopes in formats such as:

* `.csv`
* `.Wfm.csv`

The notebook handles cases where timestamps are:

* Included in the waveform file
* Not included in the waveform file

---

## Features

* Reads waveform traces from oscilloscope exports
* Handles multiple waveform formats
* Extracts voltage and timing information
* Stores processed waveforms as `.npy` files
* Organizes waveform data for later pulse analysis

---

## Input Requirements

Create a folder named:

```text
SiPM02/
```

Place all oscilloscope waveform files inside this directory.

Example:

```text
SiPM02/
├── run1.Wfm.csv
├── run2.Wfm.csv
├── test.csv
```

---

## Output

Processed waveform arrays are saved into:

```text
waveforms/
```

Each waveform is stored as a NumPy array (`.npy`) for fast loading during analysis.

---

## Typical Workflow

1. Export waveform traces from the oscilloscope
2. Copy waveform files into `SiPM02/`
3. Run `SIPM02_readfile.ipynb`
4. Generated `.npy` files are stored in `waveforms/`
5. Use these outputs in `SiPM02_Analysis_fixed.ipynb`

---

# 2. SiPM02_Analysis_fixed.ipynb

## Purpose

This notebook performs waveform pulse analysis and extracts SiPM performance parameters.

The analysis includes:

* Pulse finding
* Baseline subtraction
* Charge integration
* Peak extraction
* Histogram generation
* Gaussian fitting
* Finger plot analysis
* SPE and ECF calculations

---

## Main Analysis Features

### Waveform Processing

* Reads waveform arrays from processed data
* Computes waveform timestamps
* Identifies pulse peaks
* Measures pulse amplitude and timing

### Charge Extraction

Integrated pulse charge is calculated from the waveform data.

### Gaussian Fitting

The notebook fits Gaussian functions to histogram peaks using:

```python
curve_fit
```

This is used for:

* Pedestal fitting
* SPE peak extraction
* Charge calibration

### Finger Plot Analysis

Finger plots are used to identify discrete photoelectron peaks.

These are used to determine:

* Single photoelectron response
* Gain spacing
* Excess Charge Factor (ECF)

### Peak Detection

Peak identification is performed using:

```python
pypeaks
```

including:

* Slope-based peak finding
* Histogram peak analysis

---

## Key Quantities Extracted

| Quantity       | Description                   |
| -------------- | ----------------------------- |
| SPE            | Single photoelectron response |
| ECF            | Excess Charge Factor          |
| Average Charge | Mean integrated pulse charge  |
| Overvoltage    | Bias voltage above breakdown  |
| Peak Time      | Pulse timing information      |
| Pulse Height   | Signal amplitude              |

---

## Example Plots Generated

The notebook generates several diagnostic and physics analysis plots:

### SPE vs Voltage

Used to estimate:

* Breakdown voltage
* Gain dependence on bias voltage

### ECF vs Overvoltage

Used to study:

* Correlated noise
* Crosstalk effects

### Charge vs Voltage

Shows:

* Gain scaling
* Charge response trends

### Average Charge vs Overvoltage

Used to characterize:

* SiPM avalanche behavior
* Gain stability

### Finger Plots

Used for:

* Photoelectron peak separation
* Gain extraction
* Noise characterization

---

# Dependencies

Install the required Python packages before running the notebooks.

## Required Packages

```bash
pip install numpy pandas matplotlib scipy pypeaks
```

---

# Python Libraries Used

| Library    | Purpose                             |
| ---------- | ----------------------------------- |
| NumPy      | Numerical processing                |
| Pandas     | CSV handling                        |
| Matplotlib | Plotting                            |
| SciPy      | Curve fitting and signal processing |
| pypeaks    | Peak detection                      |
| math       | Mathematical utilities              |
| os         | File handling                       |

---

# Running the Analysis

## Step 1 — Prepare Raw Data

Place oscilloscope waveform files into:

```text
SiPM02/
```

---

## Step 2 — Convert Waveforms

Run:

```text
SIPM02_readfile.ipynb
```

This creates processed waveform arrays.

---

## Step 3 — Run Pulse Analysis

Open and run:

```text
SiPM02_Analysis_fixed.ipynb
```

The notebook will:

* Load waveform arrays
* Process pulses
* Generate histograms
* Fit SPE peaks
* Compute ECF and charge quantities
* Produce analysis plots

---

# Notes

* Ensure the waveform sampling interval and timing units are consistent.
* Baseline subtraction quality strongly affects charge extraction.
* Finger plot peak separation may depend on histogram binning.
* Cryogenic measurements may require adjusted fitting ranges and thresholds.

---

# Example Applications

This analysis framework can be used for:

* SiPM gain characterization
* Breakdown voltage estimation
* Cryogenic SiPM studies
* Low-light detector analysis
* Timing and pulse-shape studies
* Photon counting experiments
* PET detector development
* Liquid xenon detector R&D

---

# Future Improvements

Potential extensions include:

* Automated breakdown voltage fitting
* Dark count rate extraction
* Timing resolution analysis
* Multi-channel processing
* Temperature-dependent analysis
* Interactive plotting tools
* Batch processing support
* Noise filtering and waveform denoising

---

# License

This project is intended for academic and research use.



---

# Acknowledgements

Developed for SiPM waveform characterization and detector R&D studies using oscilloscope waveform acquisition and pulse analysis techniques.
