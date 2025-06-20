# LBL Stellar Template Generator

This repository provides a Python tool to generate Doppler-corrected stellar templates from FITS files, with rich metadata and documentation embedded in the output CSV files. The templates are suitable for stellar parameter analysis, including chemical composition, effective temperature, and surface gravity.

## Features

- **Relativistic Doppler Correction:** Applies a relativistic Doppler shift to the wavelength grid using the systemic velocity from FITS headers.
- **Flexible Input:** Processes multiple objects as specified in a configuration dictionary.
- **Robust Interpolation:** Uses cubic spline interpolation to resample flux and error arrays onto the shifted wavelength grid.
- **Comprehensive Metadata:** Embeds a detailed, human-readable comment block at the top of each output CSV, including instrument and object information.
- **Safe File Handling:** Skips template creation if the output file already exists.
- **Informative Logging:** Prints progress and status messages throughout processing.

## Usage

### 1. Requirements

- Python 3.8+
- `astropy`
- `numpy`
- `scipy`

Install dependencies with:

```bash
pip install astropy numpy scipy
```

### 2. Example Usage

```python
from your_module import mk_stellar_template

rparams = {
    'DATA_DIR': '/path/to/your/data',
    'OBJECT_SCIENCE': ['TYC_3980M1081M1', 'HD_123456', ...]
}

mk_stellar_template(rparams)
```

- The code expects FITS files in the following locations:
  - Masks: `{DATA_DIR}/masks/{OBJECT}_full.fits`
  - Templates: `{DATA_DIR}/templates/Template_{OBJECT}_*.fits`
- Output CSVs will be written to `{DATA_DIR}/templates/Stellar_{OBJECT}.csv`.

### 3. Output

Each output CSV file contains:
- A comment block (lines starting with `#`) with metadata and usage instructions.
- Columns: `wavelength` (µm, vacuum), `flux` (relative), `eflux` (1-sigma dispersion).

Example of reading the output in Python:

```python
from astropy.table import Table
tbl = Table.read('Stellar_TYC_3980M1081M1.csv', format='csv', comment='#')
```

## File Structure

```
your_module.py
README.md
```

## License

MIT License

## Citation

If you use this tool in your research, please cite the [LBL package](https://lbl.exoplanets.ca).

## Contact

For questions or contributions, please open an issue or contact [the LBL team](https://lbl.exoplanets.ca).
