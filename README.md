# WASP-39b Atmospheric Composition Analysis

Spectroscopic analysis of the exoplanet WASP-39b using JWST NIRSpec data to characterize atmospheric composition and estimate molecular abundances through Bayesian inference.

## Project Overview

This project analyzes James Webb Space Telescope (JWST) spectroscopic observations of WASP-39b, a hot Saturn-type exoplanet located approximately 700 light-years away. The analysis pipeline processes over 1,600 FITS file extensions, applies advanced signal processing techniques, and uses Markov Chain Monte Carlo (MCMC) methods to constrain atmospheric properties.

**Context:** This analysis was conducted shortly after the Europa Clipper mission launch, reflecting growing interest in planetary atmospheres and the potential for habitable environments beyond Earth.

## Key Features

- **Large-scale data processing**: Efficiently handled 1,611 FITS extensions from JWST MAST archive
- **Advanced spectroscopy**: Applied Savitzky-Golay filtering, binning, and residual analysis
- **Molecular detection**: Identified absorption features for CO₂, H₂O, CH₄, and Na
- **Bayesian inference**: Implemented MCMC parameter estimation using `emcee`
- **Systematic effects**: Modeled stellar contamination from star spots

## Technical Implementation

### Data Processing Pipeline

1. **FITS Data Loading** - Extract wavelength, flux, and error arrays from JWST NIRSpec observations
2. **Preprocessing** - Filter NaN values, normalize flux, and combine multiple extensions
3. **Signal Processing** - Apply Savitzky-Golay filtering (window=51, polyorder=3) for noise reduction
4. **Binning** - Aggregate data into 500 wavelength bins for efficient analysis
5. **Feature Identification** - Mark molecular absorption lines and calculate transit depths

### Atmospheric Modeling

- **Forward Model**: Simulates atmospheric transmission based on temperature and molecular abundances
- **MCMC Sampling**: 64 walkers × 5,000 steps to explore parameter space
- **Parameter Estimation**: Temperature, CO₂, H₂O, and CH₄ abundances with uncertainty quantification

### Results

**Transit Depths (Representative Values):**
- CO₂ at 4.3 µm: ~91% absorption
- CO₂ at 2.0 µm: ~86% absorption  
- H₂O at 1.4 µm: ~67% absorption
- H₂O at 2.7 µm: ~91% absorption

**Best-Fit Parameters:**
- Temperature: ~800 K
- Molecular abundances successfully constrained through MCMC

## Technologies Used

- **Python 3.9+**
- **Astropy** - FITS file handling and blackbody modeling
- **NumPy** - Numerical computations
- **SciPy** - Signal processing (Savitzky-Golay filter, binned statistics)
- **Matplotlib** - Data visualization
- **emcee** - MCMC Bayesian inference
- **scikit-image** - Image processing utilities

## Repository Structure

```
wasp39b-atmospheric-analysis/
├── wasp39b_atmospheric_analysis.ipynb  # Main analysis notebook
├── requirements.txt                     # Python dependencies
├── data/                                # Data directory (FITS files not included)
│   └── README.md                        # Data acquisition instructions
├── figures/                             # Output plots (generated on runtime)
├── CONTRIBUTORS.md                      # Project attribution and acknowledgments
└── README.md                            # This file
```

## Getting Started

### Prerequisites

- Python 3.9 or higher
- JWST FITS data files (see `data/README.md` for download instructions)

### Installation

1. Clone the repository:
```bash
git clone https://github.com/yourusername/wasp39b-atmospheric-analysis.git
cd wasp39b-atmospheric-analysis
```

2. Create a virtual environment (recommended):
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

### Usage

1. Download JWST FITS data from MAST archive (see `data/README.md`)
2. Update the `file_path` variable in the notebook to point to your FITS file
3. Run the Jupyter notebook:
```bash
jupyter notebook wasp39b_atmospheric_analysis.ipynb
```

## Data Source

JWST NIRSpec spectroscopic observations of WASP-39b from the Mikulski Archive for Space Telescopes (MAST):
- **Instrument**: NIRSpec (Near-Infrared Spectrograph)
- **Target**: WASP-39b
- **Data Type**: Transmission spectroscopy
- **Extensions**: 1,611 individual spectroscopic frames

See `data/README.md` for detailed download instructions.

## Methodology Highlights

### Data Acquisition Strategy

Rather than downloading the entire JWST dataset, we applied domain knowledge to filter observations at the source using MAST portal filters:
- Selected NIRSpec transmission spectroscopy mode
- Filtered by target name (WASP-39b)
- Chose appropriate wavelength coverage
- Downloaded only relevant FITS files

This approach demonstrates practical data engineering for large astronomical datasets.

### Key Analysis Steps

1. **Multi-Extension Processing**: Iterated through 1,611 FITS extensions, each containing a spectroscopic snapshot
2. **Noise Reduction**: Savitzky-Golay polynomial fitting preserved spectral features while smoothing noise
3. **Molecular Identification**: Cross-referenced absorption wavelengths with known molecular signatures
4. **Transit Depth Calculation**: Measured light absorption at molecular wavelengths to infer composition
5. **Forward Modeling**: Simulated atmospheric spectra using Gaussian absorption profiles
6. **Bayesian Inference**: MCMC sampled posterior distributions of atmospheric parameters

## Scientific Context

WASP-39b is a key target for JWST's exoplanet characterization program:
- **Mass**: ~0.28 Jupiter masses
- **Radius**: ~1.27 Jupiter radii
- **Temperature**: ~1,116 K (equilibrium temperature)
- **Period**: ~4.05 days

The detection of CO₂, H₂O, and other molecules provides insights into:
- Atmospheric chemistry and composition
- Cloud properties and aerosols
- Photochemistry and dynamics
- Formation history and migration

## Limitations and Future Work

- **Simplified Forward Model**: Uses Gaussian absorption profiles; could be improved with radiative transfer models
- **Systematic Effects**: Stellar spot modeling is preliminary; more sophisticated stellar contamination correction needed
- **Parameter Constraints**: MCMC convergence could be improved with longer chains or better priors
- **Molecular Lines**: Current model includes limited molecular species; could expand to CH₄, SO₂, etc.

## Project Background

This analysis originated from a graduate-level data science course focused on handling large-scale scientific datasets. The project demonstrates:
- Practical data engineering (filtering at source rather than processing everything)
- Advanced statistical methods (MCMC, Bayesian inference)
- Domain knowledge application (astronomical spectroscopy)
- Professional documentation and reproducibility

See `CONTRIBUTORS.md` for complete project context and acknowledgments.

## Acknowledgments

- JWST Science Team for making data publicly available
- Mikulski Archive for Space Telescopes (MAST) for data hosting
- Course: Projects in Data Science, [Your University]
- Inspiration: Europa Clipper mission and ongoing search for habitable worlds
- Special thanks to my course teammate for their contributions to the initial analysis

## License

This project is available for educational and research purposes.

## Contact

For questions or collaboration opportunities:
- **Name**: Niveda Giridharan
- **Email**: niveda1998@gmail.com
- **GitHub**: [@NiviGiridharan](https://github.com/NiviGiridharan)
- **LinkedIn**: [Niveda Giridharan](https://www.linkedin.com/in/niveda-giridharan-b8836217a/)

---

*This analysis was part of a graduate-level data science course focused on handling large-scale scientific datasets. The repository represents my implementation and documentation of the WASP-39b atmospheric characterization project.*
