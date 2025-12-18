# JWST Data Acquisition

## Overview

This project analyzes JWST NIRSpec spectroscopic observations of WASP-39b. The FITS files are not included in this repository due to their large size (several GB).

## How to Download the Data

### Option 1: MAST Archive Portal (Recommended)

1. Go to the MAST Portal: https://mast.stsci.edu/portal/Mashup/Clients/Mast/Portal.html

2. **Search for WASP-39b observations:**
   - In the search box, enter: `WASP-39`
   - Click "Search"

3. **Filter the results:**
   - **Mission**: Select `JWST`
   - **Instrument**: Select `NIRSPEC`
   - **Obs Type**: Select `Spectroscopy`
   - **Target Name**: `WASP-39 b` or `WASP-39b`

4. **Download the data:**
   - Select the relevant observations (look for transmission spectroscopy)
   - Click "Add to Cart" or "Download"
   - Choose the data products you need (look for `_x1d.fits` or similar spectroscopic products)

### Option 2: Direct Download (if you have the dataset ID)

If you know the specific JWST program ID:

```bash
# Example using astroquery (install first: pip install astroquery)
from astroquery.mast import Observations

# Search for WASP-39b observations
obs_table = Observations.query_criteria(
    target_name='WASP-39b',
    obs_collection='JWST',
    instrument_name='NIRSPEC/PRISM'
)

# Download data products
data_products = Observations.get_product_list(obs_table)
Observations.download_products(data_products, mrp_only=False)
```

### Option 3: Use the Exact Dataset (if known)

This analysis used JWST NIRSpec observations from a specific program. If you have the program ID:
- Visit: https://mast.stsci.edu/portal/Mashup/Clients/Mast/Portal.html
- Search by Program ID or Proposal ID
- Download the complete dataset

## Data Structure

After downloading, place the FITS file(s) in this directory:

```
data/
├── README.md (this file)
└── wasp39b_nirspec_data.fits (your downloaded file)
```

## File Format

JWST NIRSpec FITS files typically contain multiple extensions:

- **Extension 0**: Primary header
- **Extension 1**: Science header  
- **Extensions 2-1612**: Individual spectroscopic frames with columns:
  - `WAVELENGTH`: Wavelength in micrometers
  - `FLUX`: Flux values in MJy
  - `FLUX_ERROR`: Flux uncertainties

## Data Size Considerations

- **Single FITS file**: ~500 MB - 2 GB
- **Complete dataset**: Several GB

For this analysis, you only need the main spectroscopic FITS file containing the transmission spectrum.

## Filtering Strategy

Our team applied the following filtering strategy at the MAST portal to reduce data volume:

1. **Target Selection**: WASP-39b only
2. **Instrument**: NIRSpec (not NIRCam, MIRI, etc.)
3. **Mode**: Transmission spectroscopy
4. **Wavelength Coverage**: 0.5-5.0 µm (near-infrared)
5. **Data Products**: Level 2 or 3 science products (calibrated spectra)

This reduced the download from potentially hundreds of GB to a manageable ~2 GB dataset.

## Notes

- JWST data is publicly available after its proprietary period expires
- WASP-39b observations are part of JWST's Early Release Science (ERS) program
- Data quality may vary; check for calibration flags in FITS headers

## Troubleshooting

**Problem**: Cannot find WASP-39b data on MAST
- **Solution**: Try different name variants: "WASP-39 b", "WASP-39b", "WASP39b"

**Problem**: Download is too slow
- **Solution**: Use MAST's bulk download scripts or AWS S3 direct access (see MAST documentation)

**Problem**: FITS file structure doesn't match expected format
- **Solution**: Check which JWST pipeline stage the data is from (Stage 2 vs Stage 3)

## Additional Resources

- [JWST User Documentation](https://jwst-docs.stsci.edu/)
- [MAST Data Access Guide](https://mast.stsci.edu/api/v0/index.html)
- [Astropy FITS Documentation](https://docs.astropy.org/en/stable/io/fits/)
- [WASP-39b JWST ERS Program](https://ers-transit.github.io/)

## Contact

If you have trouble accessing the data, feel free to reach out or check the main README for alternative approaches.
