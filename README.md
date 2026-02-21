<br>
<p align="center">
  <h1 align="center"><strong>Novel Demonstration Generation with Gaussian Splatting Enables Robust One-Shot Manipulation</strong></h1>
  <p align="center">
    <a href='https://yangsizhe.github.io/' target='_blank'>Sizhe Yang*</a>, <a href='https://virlus.github.io/' target='_blank'>Wenye Yu*</a>, <a href='https://increase24.github.io/' target='_blank'>Jia Zeng</a>, <a href='https://lyuj1998.github.io/' target='_blank'>Jun Lv</a>, <a href='https://github.com/tongji-rkr/' target='_blank'>Kerui Ren</a>, <a href='https://www.mvig.org/' target='_blank'>Cewu Lu</a>, <a href='https://dahua.site/' target='_blank'>Dahua Lin</a>, <a href='https://oceanpang.github.io/' target='_blank'>Jiangmiao Pang</a>
    <br>
    * Equal Contributions
    <br>
    Shanghai AI Laboratory, The Chinese University of Hong Kong, Shanghai Jiao Tong University
    <br>
  </p>

  <p align="center"><strong>Robotics: Science and Systems (RSS) 2025</strong></p>
</p>

<div id="top" align="center">

[![arXiv](https://img.shields.io/badge/arXiv-2504.13175-green)](https://arxiv.org/abs/2504.13175)
[![Homepage](https://img.shields.io/badge/Homepage-%F0%9F%8C%90-blue)](https://yangsizhe.github.io/robosplat/)

</div>


https://github.com/user-attachments/assets/2e719bdd-7f97-4269-aac8-ca0b555f6e6f



## 📋 Contents

- [🔥 Highlight](#highlight)
- [🛠️ Getting Started](#getting_started)
- [🔗 Citation](#citation)
- [📄 License](#license)
- [👏 Acknowledgements](#acknowledgements)


## 🔥 Highlight <a name="highlight"></a>

**RoboSplat** is framework that leverages 3D Gaussian Splatting (3DGS) to generate novel demonstrations for RGB-based policy learning.

Starting from **a single expert demonstration** and multi-view images, our method generates diverse and visually realistic data for policy learning, enabling robust performance across **six types of generalization** (object poses, object types, camera views, scene appearance, lighting conditions, and embodiments) in the real world.

Compared to previous 2D data augmentation methods, our approach achieves **significantly better results** across various generalization types.

<img src="./asset/teaser.jpg" alt="framework" width="100%" style="position: relative;">


## 🛠️ Getting Started <a name="getting_started"></a>

### Installation

First, clone this repository.

```
git clone https://github.com/OpenRobotLab/RoboSplat.git
```

(Optional) Use conda to manage the python environment.

```
conda create -n robosplat python=3.10 -y
conda activate robosplat
```

Install dependencies.
```
# Install PyTorch according to your CUDA version. For example, if your CUDA version is 11.8:
pip install torch==2.4.1 torchvision==0.19.1 torchaudio==2.4.1 --index-url https://download.pytorch.org/whl/cu118

# Install other dependencies
pip install -r requirements.txt

# Install diff-gaussian-rasterization (adapted from https://github.com/graphdeco-inria/diff-gaussian-rasterization)
pip install third_party/diff-gaussian-rasterization

# Install PyTorch3D. If you encounter any problems, please refer to the detailed installation instructions at https://github.com/facebookresearch/pytorch3d.
cd third_party
git clone https://github.com/facebookresearch/pytorch3d.git
cd pytorch3d
conda install -c bottler nvidiacub -y
curl -LO https://github.com/NVIDIA/cub/archive/1.16.0.tar.gz
tar xzf 1.16.0.tar.gz
export CUB_HOME=$PWD/cub-1.16.0
pip install -e .  # this may take a long time
cd ../..
```


### Download Data and Assets

We provide the reconstructed and preprocessed 3D Gaussians for demonstration generation. Please follow the steps below:

- Download `data.zip` from the [Google Drive folder](https://drive.google.com/drive/folders/1zUsHHKl21251-LdehpujsUFqt36vkqQX?usp=sharing).

- Place `data.zip` in the root directory of the repository. Then, unzip it by running `unzip data.zip`.


### Usage

Generate novel demonstrations for the Pick task by running:

```
python data_aug/generate_demo.py \
    --image_size 256 \
    --save True \
    --save_video True \
    --ref_demo_path data/source_demo/real_000000.h5 \
    --xy_step_str '[10, 10]' \
    --augment_lighting False \
    --augment_appearance False \
    --augment_camera_pose False \
    --output_path data/generated_demo/pick_100
```

Description of Arguments:
- `--image_size`: (int) The size of the images in the generated demonstrations.
- `--save`: (bool) Whether to save the generated demonstrations.
- `--save_video`: (bool) Whether to save videos for visualizing the generated demonstrations.
- `--ref_demo_path`: (str) Path to the reference expert demonstration file.
- `--xy_step_str`: (str) A string in the form of '[`x`, `y`]', which specifies the density of object placement. Here, `x` is the number of object positions along the x-axis, and `y` is the number of positions along the y-axis. The total number of generated demonstrations will be `x` * `y`.
- `--augment_lighting`: (bool) Whether to apply lighting augmentation.
- `--augment_appearance`: (bool) Whether to apply appearance augmentation.
- `--augment_camera_pose`: (bool) Whether to apply camera pose augmentation.
- `--output_path`: (str) Path to save the generated demonstrations and the videos.

The code for preprocessing 3D Gaussians is available on [Google Drive](https://drive.google.com/drive/folders/1EAnD3wsMzOAqtzS2TRGgrm-B90QgPk14?usp=drive_link).


## 🔗 Citation <a name="citation"></a>

If you find our work helpful, please cite:

```bibtex
@article{robosplat,
  title={Novel Demonstration Generation with Gaussian Splatting Enables Robust One-Shot Manipulation},
  author={Yang, Sizhe and Yu, Wenye and Zeng, Jia and Lv, Jun and Ren, Kerui and Lu, Cewu and Lin, Dahua and Pang, Jiangmiao},
  journal={arXiv preprint arXiv:2504.13175},
  year={2025}
}
```


## 📄 License <a name="license"></a>

This repository is released under the [Apache 2.0 license](./LICENSE).


## 👏 Acknowledgements <a name="acknowledgements"></a>

Our code is built upon [3DGS](https://github.com/graphdeco-inria/gaussian-splatting) and [diff-gaussian-rasterization](https://github.com/graphdeco-inria/diff-gaussian-rasterization). We thank the authors for open-sourcing their code and for their significant contributions to the community.
