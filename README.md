# luxendo-h5-converter

**Convert MuVi-SPIM HDF5 (.h5) files to TIFF stacks with calibration metadata.**

---

## Overview

Luxendo H5 Converter is a Python tool for batch-converting MuVi-SPIM `.h5` files to calibrated TIFF files. It reads voxel size and other metadata from companion `.json` files and embeds this information in the TIFF output, making the files compatible with ImageJ/Fiji and other scientific imaging platforms.

---

## Features

- **Batch conversion** of `.h5` files to TIFF format
- **Reads calibration metadata** from `.json` files (voxel size: width, height, depth)
- **TIFF output** includes correct voxel size and axes information
- **Graphical user interface (GUI)** for folder selection and status feedback
- **Optional logging** of processing steps (in advanced versions)

---

## Requirements

- Python 3.7+
- `h5py`
- `tifffile`
- `tkinter` (standard with Python)
- `json` (standard with Python)

Install Python dependencies with:
```bash
pip install h5py tifffile
```

---

## Usage

### 1. Prepare Your Data

- Place your `.h5` files and their matching `.json` files in the same directory.
- Each `.h5` file should have an accompanying `.json` file containing the `"voxel_size_um"` information under `"processingInformation"`.

**Example JSON:**
```json
{
  "processingInformation": {
    "voxel_size_um": {
      "width": 0.325,
      "height": 0.325,
      "depth": 1.0
    }
  }
}
```

### 2. Run the Converter

Launch the main script:

```bash
python lightsheet-h5-converter-v4.py
```

#### GUI Steps

1. **Select input folder** containing `.h5` and `.json` files.
2. **Select output folder** for the converted `.tiff` files.
3. The status window will show progress, found files, and voxel dimensions.

---

## Output

- Converted `.tiff` files are named after their input `.h5` files.
- TIFF metadata includes:
  - Voxel size (`width`, `height`, `depth`)
  - Axes (`ZYX`)
  - Unit (`um`)
- TIFFs are compatible with ImageJ/Fiji.

---

## Troubleshooting

- Make sure each `.h5` file has a corresponding `.json` file with valid voxel size information.
- Only `.h5` files with a `Data` dataset are supported.
- Check folder permissions if conversion fails.
- Large files may require substantial RAM.

---

## Advanced Options (v4 only)

- **Process subfolders:** Optionally converts `.h5` files in subdirectories.
- **Custom output directory:** Specify where to save TIFF files.

---

## Example Workflow

1. Place `sample.h5` and `sample.json` in a folder.
2. Run `python lightsheet-h5-converter-v4.py`.
3. Select your data folder and desired output folder.
4. Monitor status window for conversion progress.
5. Find the converted `sample.tiff` in the output folder.

---

## References

- Main script: [`lightsheet-h5-converter-v4.py`](https://github.com/Daniel-Waiger/luxendo-h5-converter/blob/main/lightsheet-h5-converter-v4.py)
- Previous versions: [`old/`](https://github.com/Daniel-Waiger/luxendo-h5-converter/tree/main/old)

---

## Contact

For questions or issues, please [open an issue](https://github.com/Daniel-Waiger/luxendo-h5-converter/issues).
