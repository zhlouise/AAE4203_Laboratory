# AAE4203 Laboratory – GNSS Positioning and Analysis

## 1. Overview
This repository contains code, data, and figures supporting the AAE4203 laboratory investigation into standalone single point positioning (SPP), weighted least squares estimation (WLSE), and real‑time kinematic (RTK) GNSS positioning. It includes:
- Raw and processed GNSS observation files
- Python and MATLAB scripts for data conversion, estimation, and analysis
- Resulting position and error datasets
- Figures used in the lab report
- An embedded MATLAB wrapper for RTK/MALIB functionality (`MatRTKLIB-main`)

The full laboratory report is provided in:  
`AAE4203_Lab_Report.pdf`

## 2. Lab Objectives
(TODO: Summarize the experimental goals. Example bullets below.)
- Quantify positioning accuracy of SPP vs. WLSE vs. RTK solutions
- Assess error sources (ionospheric delay, multipath, satellite geometry)
- Evaluate ambiguity resolution success criteria
- Compare kinematic vs. static positioning performance

## 3. Experimental Setup
(TODO: Describe receiver hardware, antenna, environment, observation duration, constellations enabled, sampling interval, reference station info if RTK used.)

## 4. Repository Structure

| Path / File | Purpose |
|-------------|---------|
| `AAE4203_Lab_Report.pdf` | Formal written lab report (reference for narrative sections) |
| `Data/` | Raw or intermediate GNSS/RINEX data inputs (TODO: enumerate key files) |
| `Figures/` | Generated plots used in the report (error time series, constellations, residuals, etc.) |
| `estimated_positions.csv` | Computed position estimates (likely ECEF or LLH); used for accuracy evaluation |
| `positioning_errors.csv` | Derived error metrics (e.g., ENU deviations, RMS) |
| `WLSE_SPP.py` | Python implementation of Weighted Least Squares Single Point Positioning |
| `WLSE_SPP_Solutions/` | Output artifacts from WLSE/SPP processing (TODO: describe contents) |
| `RTKLIB_RTK_Solution/` | RTK solution output files (e.g., position time series, status flags) |
| `pyubx2_csv_converter_gui.py` | GUI utility for converting UBX receiver data to CSV |
| `rinex2csv.m` | MATLAB script for converting RINEX observation files to CSV for downstream processing |
| `MatRTKLIB-main/` | MATLAB wrapper around MALIB/RTKLIB functionality (port + tools) |
| `MatRTKLIB-main/+gt/README.md` | Documentation of GNSS Tools (GT) MATLAB classes |
| `MatRTKLIB-main/examples/README.md` | List of example MATLAB scripts (positioning, editing, analysis) |
| `MatRTKLIB-main/README.md` | Upstream project documentation (features, compilation, citation status) |

## 5. Dependencies
- MATLAB
- MALIB / RTKLIB (via `MatRTKLIB-main`)
- Python (for WLSE script, pyubx2 converter)
- `pyubx2` (if using UBX conversion GUI)

## 6. AI Assistance Acknowledgement
Portions of this README (structure, wording, and placeholder scaffolding) were generated with assistance from an AI tool (GitHub Copilot Chat). 
