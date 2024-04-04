# Lab-project : using Segment Anything (SAM) to segment cancer cells in H&E Images
This repository contains the code implementation of our lab project which consists of investigating how [SAM](https://github.com/facebookresearch/segment-anything.git) can be leveraged for automatic cancer cell detection in H&E images. 

Specifically, our contribution is tow-fold:
1. We show how te perftomances of SOTA model [Hovernet](https://github.com/vqdang/hover_net.git) can be imporved with SAM used as a post-processing 
2. We combine the efforts made in the works of [MedSAM](https://github.com/bowang-lab/MedSAM.git) and [CellViT](https://github.com/TIO-IKIM/CellViT.git) to slightly improve the SOTA performances in cell-segmentation.   

Both experiments are made on the [PanNuke](https://warwick.ac.uk/fac/cross_fac/tia/data/pannuke) dataset, a challenging nuclei instance segmentation benchmark.
