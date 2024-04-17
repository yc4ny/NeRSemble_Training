# Preprocessing and Training NeRSemble Dataset on Gaussian Head Avatars

## Requirements

* Create a conda environment.
```
conda env create -f environment.yaml
conda activate gha
```
* Install [Pytorch3d](https://github.com/facebookresearch/pytorch3d).
```
pip install --no-index --no-cache-dir pytorch3d -f https://dl.fbaipublicfiles.com/pytorch3d/packaging/wheels/py38_cu113_pyt1120/download.html
```
* Install [kaolin](https://github.com/NVIDIAGameWorks/kaolin).
```
pip install kaolin==0.13.0 -f https://nvidia-kaolin.s3.us-east-2.amazonaws.com/torch-1.12.0_cu113.html
```
* Install diff-gaussian-rasterization and simple_knn from [gaussian-splatting](https://github.com/graphdeco-inria/gaussian-splatting). Note, for rendering 32-channel images, please modify "NUM_CHANNELS 3" to "NUM_CHANNELS 32" in "diff-gaussian-rasterization/cuda_rasterizer/config.h".
```
git clone git@github.com:graphdeco-inria/gaussian-splatting.git --recursive
cd gaussian-splatting
# Modify "submodules/diff-gaussian-rasterization/cuda_rasterizer/config.h"
pip install submodules/diff-gaussian-rasterization
pip install submodules/simple-knn
cd ..
```
* Download Required Files and Checkpoints
```
gdown --folder https://drive.google.com/drive/folders/1DwlumiyUrxm6DJDqnGcaqTae8O0uoSxZ?usp=sharing
mv assets/BFM09_model_info.mat Multiview-3DMM-Fitting/assets/BFM/
mv assets/pytorch_resnet101.pth BackgroundMattingV2/assets/
```

**Overview 

The codebase has 6 main components.
- Step 1: Extracting frames from raw videos and resizing, cropping to match input of Gaussian-Head-Avatars. 
- Step 2: Sampling Data. Every 10th frame is sampled and used for training. 
- Step 3: Performing Background Removal using [BackgroundMattingV2](https://github.com/PeterL1n/BackgroundMattingV2)
- Step 4: Performing Multiview BFM 2D Keypoing Detection + Parameter Fitting
- Step 5: Training - Stage 1: Geometry Guided Initialization 
- Step 6: Training - Stage 2: Gaussian Head Avatar Model


## Datasets
In this code's pipeline instructions for preprocessing [NeRSemble dataset](https://tobias-kirschstein.github.io/nersemble/):
* Apply to download [NeRSemble dataset](https://tobias-kirschstein.github.io/nersemble/) and unzip it into "path/to/raw_NeRSemble/".



## Citation
```
@inproceedings{xu2023gaussianheadavatar,
  title={Gaussian Head Avatar: Ultra High-fidelity Head Avatar via Dynamic Gaussians},
  author={Xu, Yuelang and Chen, Benwang and Li, Zhe and Zhang, Hongwen and Wang, Lizhen and Zheng, Zerong and Liu, Yebin},
  booktitle={Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR)},
  year={2024}
}