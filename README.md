# Lab-project : using Segment Anything (SAM) to segment cancer cells in H&E Images
This repository contains the code implementation of our lab project which consists of investigating how [SAM](https://github.com/facebookresearch/segment-anything.git) can be leveraged for automatic cancer cell detection in H&E images. 

Specifically, our contribution is two-fold:
1. We show how te performances of SOTA model [Hovernet](https://github.com/vqdang/hover_net.git) can be improved with SAM used as a post-processing 
2. We combine the efforts made in the works of [MedSAM](https://github.com/bowang-lab/MedSAM.git) and [CellViT](https://github.com/TIO-IKIM/CellViT.git) to slightly improve the SOTA performances in automated instance segmentation of cell nuclei in digitized tissue samples. More specifically, we use the weights of the ViT encoder from MedSAM in the training of CellViT.

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
### Pannuke dataset prepration
To preprocess the pannuke dataset in order to have the right input for the model, il faut convertir le Pannuke dataset qui orginellement est dans le format suivant:

```
├── fold0
│   ├── images.npy
│   ├── masks.npy
│   └── types.npy
├── fold1
│   ├── images.npy
│   ├── masks.npy
│   └── types.npy
└── fold2
    ├── images.npy
    ├── masks.npy
    └── types.npy
```
en un dataset du format suivant qui est plus adéquat au multithreading and l'application de data augmentation:

```
├── fold0
│   ├── cell_count.csv      # cell-count for each image to be used in sampling
│   ├── images              # H&E Image for each sample as .png files
│   ├── images
│   │   ├── 0_0.png
│   │   ├── 0_1.png
│   │   ├── 0_2.png
...
│   ├── labels              # label as .npy arrays for each sample
│   │   ├── 0_0.npy
│   │   ├── 0_1.npy
│   │   ├── 0_2.npy
...
│   └── types.csv           # csv file with type for each image
├── fold1
│   ├── cell_count.csv
│   ├── images
│   │   ├── 1_0.png
...
│   ├── labels
│   │   ├── 1_0.npy
...
│   └── types.csv
├── fold2
│   ├── cell_count.csv
│   ├── images
│   │   ├── 2_0.png
...  
│   ├── labels  
│   │   ├── 2_0.npy
...  
│   └── types.csv  
├── dataset_config.yaml     # dataset config with dataset information
└── weight_config.yaml      # config file for our sampling
```

Afin de convertir les données dans le bon format, nous vous invitions à run les commandes suivantes depuis le dossier (~/CellViT/cell_segmentation/dataset) : 

```
python prepare_pannuke.py --input_path (original Pannuke dataset path) --output_path (processed Pannuke dataset path)
```

## Training

### Training from scratch
To replicate the results presented in our report from scratch, you will first need to download the weights of the classical SAM encoder wieghts (i.e. SAM-ViT-B) and the MedSAM encoder weights (i.e. MedSAM-ViT-B) , which you can find at this [link](https://drive.google.com/drive/folders/1HKZUDm1SZejdVYZKlbb8ufsACjfx8Pcd?usp=drive_link)

Pour lancer l'entrainement de CellVit avec SAM-ViT-B, nous vous invitons, en premier lieu à 



une fois que vous vous trouvez dans le dossier (~/CellViT/cell_segmentation), a éffectuer la ligne  de commande suivantes:

``` usage: run_cellvit.py [-h] --config CONFIG [--gpu GPU] [--sweep | --agent AGENT | --checkpoint CHECKPOINT]

Start an experiment with given configuration file.

optional arguments:
  -h, --help            show this help message and exit
  --gpu GPU             Cuda-GPU ID (default: None)
  --sweep               Starting a sweep. For this the configuration file must be structured according to WandB sweeping. Compare
                        https://docs.wandb.ai/guides/sweeps and https://community.wandb.ai/t/nested-sweep-configuration/3369/3 for further
                        information. This parameter cannot be set in the config file! (default: False)
  --agent AGENT         Add a new agent to the sweep. Please pass the sweep ID as argument in the way entity/project/sweep_id, e.g.,
                        user1/test_project/v4hwbijh. The agent configuration can be found in the WandB dashboard for the running sweep in
                        the sweep overview tab under launch agent. Just paste the entity/project/sweep_id given there. The provided config
                        file must be a sweep config file.This parameter cannot be set in the config file! (default: None)
  --checkpoint CHECKPOINT
                        Path to a PyTorch checkpoint file. The file is loaded and continued to train with the provided settings. If this is
                        passed, no sweeps are possible. This parameter cannot be set in the config file! (default: None)

required named arguments:
  --config CONFIG       Path to a config file (default: None)
```

## Checkpoints to download 

Checkpoints for [medsam_vit_b](
Checkpoints for SAM_vit_b


### Training on the Pannuke dataset




## Checkpoints to download 

## Dataset preparation

## 








