# FPGA Deployment of Iris Classification Model

This repository showcases the implementation of a machine learning classifier for the Iris dataset, specifically optimized for Field-Programmable Gate Array (FPGA) deployment through `hls4ml`. The neural network undergoes quantization and pruning techniques to ensure efficient FPGA resource utilization.

## Installation

Initialize the development environment by installing all required dependencies:

```bash
poetry install
```

**Important:** Expect a lengthy installation process due to comprehensive machine learning frameworks including TensorFlow and PyTorch.

## Execution

Launch the complete model development and deployment pipeline:

```bash
poetry run buildmodel
```

This executes the `BuildModel` module, orchestrating the full workflow from data preparation through FPGA bitstream creation.

## Repository Organization

- **`.gitignore`**: Git exclusion rules for temporary and generated files.
- **`pyproject.toml`**: Poetry configuration with project metadata and dependency specifications.
- **`utilities/on_target.py`**: Target board execution script for loading test data and performing inference.
- **`classification_model_on_fpgas/BuildModel.py`**: Core module managing the end-to-end pipeline from dataset handling to FPGA preparation.
- **`classification_model_on_fpgas/__init__.py`**: Package initialization file.

## Pipeline Overview

The `BuildModel` module executes the following workflow:

1. **Data Preparation**: Acquires the Iris dataset, applies preprocessing transformations, creates train/test splits, and persists test samples.
2. **Model Development**: Constructs a quantized neural network architecture, applies structured pruning for size optimization, and trains on the prepared dataset.
3. **Hardware Generation**: Transforms the Keras model into HLS-compatible format via `hls4ml`, performs synthesis, and produces the FPGA bitstream.
4. **Deployment Preparation**: Aggregates all deployment artifacts (bitstream, hardware handoff files, driver utilities) into the `package` directory.
5. **Target Transfer**: (Optional) Deploys prepared files to the destination FPGA board using secure copy protocol.

## Target Board Execution

After successful file transfer to the FPGA board, execute the inference script:

```bash
python on_target.py
```

The script performs:
- Test dataset loading
- FPGA bitfile configuration
- Model inference execution and result persistence

## Model Verification
Model validation occurs before hardware synthesis to ensure accuracy preservation. The console output displays comparative metrics:
```
Accuracy of the original pruned and quantized model: 93.33%
Accuracy of the HLS model: 93.33%
```

## Technology Stack

This project leverages Poetry for dependency management with the following key components:

- Machine learning frameworks: `tensorflow`, `torch`, `scikit-learn`
- FPGA optimization: `hls4ml`, `qkeras` 
- Hardware interface: `pynq`
- Development environment: Various Jupyter ecosystem packages

Complete dependency specifications are available in `pyproject.toml`.

## Licensing

This project operates under the MIT License terms.

## Maintainer
Sameer Suleman
