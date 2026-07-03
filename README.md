---
title: Mass Spec AUC Analysis
emoji: 🧪
colorFrom: blue
colorTo: green
sdk: gradio
app_file: main.py
pinned: false
---
# Mass Spectrometry Area Under Curve (AUC) Analysis

A web-based application for analyzing exported mass spectrometry spectra and calculating area under the curve (AUC) for selected m/z ranges.

## Features

- **CSV and TXT file support**: Upload exported spectra as `.csv` or `.txt` files.
- **Multiple file analysis**: Upload several spectra at once and calculate the same m/z ranges for every file.
- **Custom ranges**: Choose how many m/z ranges to add, then fill only those range boxes.
- **Spectrum visualization**: Plot the spectrum with colored regions for the selected ranges.
- **Spectrum selector**: Choose which uploaded spectrum to display in the plot.
- **Spectrum close-up**: Optionally choose the m/z window shown in the plot.
- **Results table**: View one row per file with one area column per selected range.
- **Export results**: Download the calculated table as a CSV file.

## Installation

### Prerequisites

- Python 3.7 or higher
- pip package manager

### Setup

1. Clone or download this repository.
2. Navigate to the project directory:

   ```bash
   cd MS-analysis
   ```

3. Install required dependencies:

   ```bash
   pip install -r requirements.txt
   ```

## Usage

Start the Gradio web interface:

```bash
python main.py
```

This will launch a web server at `http://localhost:7860`.

### Using the Application

1. **Upload Data**: Select one or more `.csv` or `.txt` spectra files.
2. **Validate Files**: Check that the files can be read and view the combined m/z bounds.
3. **Define m/z Ranges**: Choose how many ranges to add, then enter start m/z, end m/z, and a name for each range.
4. **Choose Plot Close-Up**: Optionally enter the start and end m/z values for the spectrum image zoom.
5. **Analyze**: Generate the plot and calculations.
6. **Choose Spectrum**: Use the selector near the spectrum picture to choose which uploaded spectrum to show.
7. **Download**: Export the results table as a CSV file.

## Data Format

### TXT Files

TXT files should contain two columns separated by spaces or tabs:

- **Column 1**: m/z values
- **Column 2**: intensity values

Example:

```text
2959.5 100
2960.1 250
2960.7 1500
3279.0 50
```

### CSV Files

CSV files should contain two columns:

- **Column 1**: m/z values
- **Column 2**: intensity values

The reader supports common exported spectra files where the first 8 lines are metadata and the data starts on line 9. It also supports ordinary two-column CSV files.

## Example Ranges

| Range Name | m/z Start | m/z End | Color |
|-----------|-----------|---------|-------|
| WT-WT1 | 3268.0 | 3279.0 | Blue |
| WT-H43R1 | 3114.0 | 3123.0 | Orange |
| H43R-H43R1 | 2959.5 | 2967.0 | Green |

## Technical Details

### Files

- **main.py**: Gradio web application interface.
- **auc.py**: Core file reading, AUC calculation, plotting, and summary table functions.
- **requirements.txt**: Python package dependencies.

### Calculation Method

- **Integration**: Trapezoidal rule for numerical integration.
- **Area Calculation**: Calculates the area under the intensity curve inside each selected m/z range.
- **Multiple Files**: Applies the same user-defined ranges to every uploaded file.
- **Output Table**: Shows only the individual range areas, without automatic WT/MUT total columns.

## Troubleshooting

### File Upload Issues

- Ensure every file is `.csv` or `.txt`.
- Ensure each file contains two numeric columns: m/z and intensity.
- For CSV exports with metadata, make sure the numeric data starts after the metadata block.

### Calculation Issues

- Verify the m/z values in your selected ranges exist in the uploaded spectra.
- Check for missing or invalid data points.
- Ensure intensity values are numeric.
- Ensure each range has a start, end, and name.

## Requirements

See `requirements.txt` for Python package requirements. Key packages:

- `pandas`: Data manipulation
- `numpy`: Numerical operations
- `scipy`: Numerical integration
- `matplotlib`: Plotting
- `gradio`: Web interface

## Author

Created for mass spectrometry analysis at Weizmann Institute of Science.
