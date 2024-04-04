# Lab-project : using Segment Anything (SAM) to segment cancer cells in H&E Images
This repository contains the code implementation of our lab project which consists of investigating how [SAM](https://github.com/facebookresearch/segment-anything.git) can be leveraged for automatic cancer cell detection in H&E images. 

Specifically, our contribution is two-fold:
1. We show how te performances of SOTA model [Hovernet](https://github.com/vqdang/hover_net.git) can be improved with SAM used as a post-processing 
2. We combine the efforts made in the works of [MedSAM](https://github.com/bowang-lab/MedSAM.git) and [CellViT](https://github.com/TIO-IKIM/CellViT.git) to slightly improve the SOTA performances in automated instance segmentation of cell nuclei in digitized tissue samples. 

Both experiments are made on the [PanNuke](https://warwick.ac.uk/fac/cross_fac/tia/data/pannuke) dataset, a challenging nuclei instance segmentation benchmark.

## Installation

Clone the repository: ``` git clone https://github.com/olavdc/Lab-project.git ```
Pip install the requirements : ``` pip install -r requirements. txt ```

## Usage

### Project structure

```
├── base_ml               # Basic Machine Learning Code: CLI, Trainer, Experiment, ...
├── cell_segmentation     # Cell Segmentation training and inference files
│   ├── datasets          # Datasets (PyTorch)
│   ├── experiments       # Specific Experiment Code for different experiments
│   ├── inference         # Inference code for experiment statistics and plots
│   ├── trainer           # Trainer functions to train networks
│   ├── utils             # Utils code
│   └── run_xxx.py        # Run file to start an experiment
├── configs               # Config files
│   ├── examples          # Example config files with explanations
│   └── python            # Python configuration file for global Python settings
├── datamodel             # Datamodels of WSI, Patientes etc. (not ML specific)
├── docs                  # Documentation files (in addition to this main README.md)
├── models                # Machine Learning Models (PyTorch implementations)
│   ├── encoders          # Encoder networks (see ML structure below)
│   ├── pretrained        # Checkpoint of important pretrained models (needs to be downloaded from Google drive)
│   └── segmentation      # CellViT Code
├── preprocessing         # Preprocessing code
│   └── patch_extraction  # Code to extract patches from WSI
```








