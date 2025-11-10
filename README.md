# AAE4203 Laboratory: GNSS SPP and RTK Toolkit

Tools, data, and example workflows for GNSS signal processing as used in AAE 4203 labs, including:
- Single Point Positioning (SPP) with Weighted Least Squares Estimation (WLSE)
- Data preparation utilities for UBX and RINEX
- Reference/benchmark solutions using RTKLIB
- Plotting and comparative analysis

This repository is organized to help you prepare GNSS datasets, run an SPP solver, and compare against RTK solutions. Figures and plots are generated into the Plots directory and can be used directly in reports.

## Repository structure

- [Data/](Data)  
  Input and intermediate datasets. Place your raw and converted CSV/RINEX/UBX-derived files here.

- [MatRTKLIB-main/](MatRTKLIB-main)  
  MATLAB utilities related to RTKLIB workflows and analysis.

- [Plots/](Plots)  
  Generated figures and plots for lab analysis and reports.

- [RTKLIB_RTK_Solution/](RTKLIB_RTK_Solution)  
  RTKLIB-based reference/benchmark outputs for comparison with SPP.

- [WLSE_SPP.py](WLSE_SPP.py)  
  Python implementation of a Weighted Least Squares Estimator for Single Point Positioning (SPP).

- [WLSE_SPP_Solutions/](WLSE_SPP_Solutions)  
  Saved solution outputs from SPP runs (e.g., positions, residuals, summaries).

- [pyubx2_csv_converter_gui.py](pyubx2_csv_converter_gui.py)  
  A small GUI utility to convert UBX logs to CSV using pyubx2.

- [rinex2csv.m](rinex2csv.m)  
  MATLAB script to convert RINEX observations to CSV for downstream processing.

## Prerequisites

- Python 3.9+ (tested with modern Python versions)
- MATLAB R2021a+ (or comparable version for running MATLAB scripts)
- Recommended OS: Windows, macOS, or Linux

### Python packages
Install the common dependencies:
```bash
pip install numpy pandas scipy matplotlib pyubx2
```
Optional but useful:
```bash
pip install seaborn jupyter
```

## Quick start

### 1) Clone the repository
```bash
git clone https://github.com/zhlouise/AAE4203_Laboratory.git
cd AAE4203_Laboratory
```

### 2) Prepare your data

You can start from either UBX or RINEX sources.

- UBX → CSV using the GUI converter:
  ```bash
  python pyubx2_csv_converter_gui.py
  ```
  Use the GUI to select your UBX file(s) and export to CSV. Save outputs into [Data/](Data).

- RINEX → CSV using MATLAB:
  1. Open MATLAB in the repo folder.
  2. Run the converter with your paths:
     ```matlab
     % rinex2csv.m has example usage in the file header/comments.
     % Example:
     rinex2csv('Data/your_obs.21o', 'Data/your_obs.csv');
     ```
  3. Verify the CSV appears in [Data/](Data).

Tips:
- Keep a consistent naming convention for input and output files.
- Ensure timestamps are in consistent formats (UTC/GPS) across sources before combining.

### 3) Run the WLSE SPP solver
The [WLSE_SPP.py](WLSE_SPP.py) script performs Single Point Positioning using weighted least squares. Typical inputs include pseudorange observations and satellite metadata derived from your conversions.

Common patterns to run:
```bash
python WLSE_SPP.py
```

Notes:
- If the script relies on in-file configuration, open `WLSE_SPP.py` and edit the input paths/parameters near the top (e.g., input CSV filenames, sampling rate, mask angles, weighting scheme).
- If command-line arguments are supported, run with `-h` or `--help` to see usage details.

Expected outputs:
- Numerical solutions (estimated receiver positions, clock bias)
- Residuals and quality metrics
- Plots saved to [Plots/](Plots)
- Solution files saved to [WLSE_SPP_Solutions/](WLSE_SPP_Solutions)

### 4) Compare with RTKLIB solutions
Use the results in [RTKLIB_RTK_Solution/](RTKLIB_RTK_Solution) as a reference/benchmark:
- Overlay SPP trajectories with RTKLIB solutions to assess accuracy
- Review convergence behavior, outliers, and dilution of precision (DOP)
- Summarize differences in horizontal/vertical error and scatter

## Workflow overview

1. Acquire raw GNSS data (UBX or RINEX).
2. Convert to CSV:
   - UBX → CSV via `pyubx2_csv_converter_gui.py`
   - RINEX → CSV via `rinex2csv.m`
3. Configure and run SPP in `WLSE_SPP.py`.
4. Review generated plots in [Plots/](Plots) and numerical outputs in [WLSE_SPP_Solutions/](WLSE_SPP_Solutions).
5. Compare with RTK results in [RTKLIB_RTK_Solution/](RTKLIB_RTK_Solution).

## Figures and plots

Generated figures are saved into [Plots/](Plots). These typically include:
- Position scatter plots (top-down)
- East/North/Up time series
- Residual histograms and time series
- DOP metrics over time

You can embed figures from the Plots directory into your lab reports. If you regenerate results, existing figures may be overwritten—consider versioned filenames when running multiple experiments.

## Data format expectations

While formats depend on your conversion scripts, typical CSV columns for SPP include:
- Time tags (e.g., GPS week/seconds or UTC timestamps)
- Satellite PRNs and constellation IDs
- Pseudoranges and signal quality indicators (e.g., C/N0)
- Satellite positions/ephemeris-derived states (or access to ephemeris to compute them)
- Optional: Elevation/azimuth angles, tropospheric/ionospheric models parameters, weights

Ensure units and reference frames are consistent across inputs (e.g., meters for ranges, WGS84/ITRF for positions).

## Notes on WLSE weighting and models

- Weighting schemes often use elevation-dependent models or C/N0-based weights.
- Corrections may include:
  - Receiver clock bias
  - Tropospheric delay (e.g., Saastamoinen)
  - Ionospheric delay (e.g., Klobuchar for single-frequency)
  - Earth rotation and relativistic effects
- Mask angles and outlier rejection significantly affect solution stability.

Consult `WLSE_SPP.py` inline documentation/comments to confirm the models implemented.

## Troubleshooting

- No plots produced:
  - Check input file paths inside `WLSE_SPP.py`.
  - Confirm your Python environment has matplotlib/seaborn.
- Empty or malformed solutions:
  - Verify CSV column names and units match what the script expects.
  - Ensure time systems align (GPS vs UTC) and leap seconds are handled.
- RINEX conversion errors:
  - Confirm RINEX version compatibility with `rinex2csv.m`.
  - Inspect the MATLAB console for parsing issues in headers or observation blocks.
- UBX conversion issues:
  - Try a smaller UBX segment first.
  - Confirm `pyubx2` supports your receiver’s message types/firmware.

## Acknowledgements

- RTKLIB and related MATLAB tools inspired workflows in [MatRTKLIB-main/](MatRTKLIB-main).
- [pyubx2](https://github.com/semuconsulting/pyubx2) for UBX parsing and conversion.
- GNSS community resources for SPP modeling references.

## How to cite

If you use or adapt parts of this repository for reports or publications, consider citing:
- This repository (commit/branch used)
- RTKLIB
- pyubx2
- Any specific models (troposphere/ionosphere) or datasets used

## Contact

For questions or suggestions, please open an issue or reach out to [@zhlouise](https://github.com/zhlouise).

---
Last updated: 2025-11-10
