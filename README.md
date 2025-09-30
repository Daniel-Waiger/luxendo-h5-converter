# Luxendo H5 Converter

A Python GUI application for converting MuVi-SPIM H5 files to calibrated TIFF stacks with proper metadata preservation.

## Overview

This tool converts 3D microscopy data from Luxendo MuVi-SPIM systems stored in HDF5 (.h5) format to TIFF stacks. It preserves spatial calibration information by reading voxel dimensions from accompanying JSON metadata files and embedding this information into the output TIFF files for proper visualization in ImageJ and other image analysis software.

## Features

- **GUI Interface**: User-friendly graphical interface with real-time processing status
- **Batch Processing**: Process single folders or recursively process all subfolders
- **Metadata Preservation**: Reads voxel dimensions from JSON files and embeds them in TIFF metadata
- **ImageJ Compatibility**: Outputs ImageJ-compatible TIFF stacks with proper calibration
- **Progress Tracking**: Real-time status updates and comprehensive logging
- **Memory Management**: Built-in garbage collection for processing large datasets

## Requirements

### System Requirements
- Python 3.6 or higher
- Operating System: Windows, macOS, or Linux with GUI support

### Python Dependencies
- `h5py` - For reading HDF5 files
- `tifffile` - For writing calibrated TIFF files
- `tkinter` - For the graphical user interface (usually included with Python)
- `json` - For reading metadata files (built-in)
- `logging` - For process logging (built-in)
- `gc` - For memory management (built-in)
- `os` - For file system operations (built-in)

### Installation

1. **Install Python Dependencies:**
   ```bash
   pip install h5py tifffile
   ```

2. **Download the Converter:**
   Download `lightsheet-h5-converter-v4.py` from this repository.

3. **Verify Installation:**
   Run the script to ensure all dependencies are available:
   ```bash
   python lightsheet-h5-converter-v4.py
   ```

## Input File Requirements

The converter requires two types of files for each dataset:

### 1. HDF5 Data File (.h5)
- Contains the 3D image data in a dataset named `'Data'`
- Standard HDF5 format as exported by MuVi-SPIM systems
- Must have a corresponding JSON metadata file

### 2. JSON Metadata File (.json)
The JSON file must contain voxel dimension information in the following structure:
```json
{
  "processingInformation": {
    "voxel_size_um": {
      "width": 0.5,
      "height": 0.5,
      "depth": 1.0
    }
  }
}
```

**File Naming Convention:**
- JSON files should contain the base name of the corresponding H5 file
- Example: `sample_data.h5` pairs with `sample_data_metadata.json`

## Usage Instructions

### Starting the Application

1. **Run the Script:**
   ```bash
   python lightsheet-h5-converter-v4.py
   ```

2. **GUI Interface:**
   A window will open showing:
   - Processing status text area
   - Current file information display
   - Voxel dimensions display
   - Two processing mode buttons

### Processing Modes

#### Single Folder Processing
1. Click **"Process Single Folder"**
2. Select the input folder containing H5 and JSON files
3. Select the output folder for converted TIFF files
4. Processing will begin automatically

#### Subfolder Processing
1. Click **"Process All Subfolders"**
2. Select the root input folder
3. The tool will recursively process all subfolders
4. TIFF files are saved in the same location as source H5 files

### Processing Workflow

For each H5 file found, the converter:

1. **Locates Matching JSON File:** Searches for JSON file with matching base name
2. **Reads Voxel Dimensions:** Extracts spatial calibration from JSON metadata
3. **Loads H5 Data:** Reads the 3D dataset from the 'Data' group
4. **Converts to TIFF:** Saves as ImageJ-compatible TIFF stack with:
   - Proper voxel spacing metadata
   - Micrometer units
   - ZYX axis order
   - Creator information

### Output Files

- **Format:** TIFF stack (.tiff)
- **Naming:** Same as input H5 file with .tiff extension
- **Metadata:** Includes spatial calibration, units, and axis information
- **Compatibility:** ImageJ, FIJI, and other image analysis software

## Status Window Information

The GUI provides real-time feedback:

- **Processing Status:** Shows current operation and progress
- **Files Found:** Displays current H5 and JSON file pair
- **Voxel Dimensions:** Shows extracted spatial calibration values
- **Processing Log:** Detailed status messages with timestamps

## Logging

The application creates a log file `processing_log.txt` in the current directory, containing:
- Timestamp for each operation
- File processing status
- Error messages and warnings
- Processing completion notifications

## Troubleshooting

### Common Issues

#### "No JSON metadata file found"
- **Cause:** Missing or incorrectly named JSON file
- **Solution:** Ensure JSON file name contains the H5 file's base name

#### "Key 'voxel_size_um' not found"
- **Cause:** JSON file doesn't contain required metadata structure
- **Solution:** Verify JSON file has the correct `processingInformation.voxel_size_um` structure

#### "No 'Data' dataset found"
- **Cause:** H5 file doesn't contain expected data structure
- **Solution:** Verify the H5 file contains a dataset named 'Data' at the root level

#### Memory Issues with Large Files
- **Cause:** Insufficient RAM for large 3D datasets
- **Solution:** Process files individually or use a machine with more RAM

### Error Messages

The application provides detailed error messages in both the GUI and log file. Common patterns:

- **File Access Errors:** Check file permissions and paths
- **Format Errors:** Verify file integrity and format compliance
- **Memory Errors:** Monitor system resources during processing

## Technical Details

### Data Processing Pipeline

1. **File Discovery:** Recursively scans directories for .h5 files
2. **Metadata Extraction:** Parses JSON files for voxel dimensions
3. **Data Loading:** Reads 3D arrays from HDF5 'Data' dataset
4. **Format Conversion:** Converts to ImageJ-compatible TIFF format
5. **Metadata Embedding:** Includes spatial calibration in TIFF metadata

### Metadata Preservation

The converter preserves the following information:
- **Voxel Spacing:** X, Y, Z dimensions in micrometers
- **Units:** Micrometer specification
- **Axis Order:** ZYX (depth, height, width)
- **Resolution:** X/Y pixel resolution for ImageJ
- **Creator Information:** Software attribution

### Memory Management

- **Garbage Collection:** Automatic memory cleanup after each file
- **Streaming Processing:** Files processed individually to minimize memory usage
- **Resource Cleanup:** Proper closing of file handles and GUI resources

## Version History

- **v4 (Current):** GUI interface with dual processing modes and enhanced error handling
- **v3:** Added metadata preservation and improved file handling
- **v2:** Basic conversion functionality with JSON metadata support
- **v1:** Initial H5 to TIFF conversion

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Author

Created by Daniel Waiger with GPT-4 assistance.

## Support

For issues, questions, or contributions, please use the GitHub repository's issue tracker.
