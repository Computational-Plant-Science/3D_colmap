# 3D modeing pipeline using Colmap

Pipeline: Build 3D root models from images captured by 3D root scanner.

This repo was to reconstruct a 3D point cloud root model from images captured by our 3D root scanner or portable scanner in the field.
 
For example, images are captured by our 3D root scanner with 10 cameras mouting on a rotating arm. 

![3D root scanner prototype](../main/media/3D_scanner.gif)

a real root sample and its 3D reconstruction point cloud model was compared side by side:

![3D root model reconstruction](../main/media/3D_model.gif)


Our upgraded portable scanner can capture around 240 images in 7 mins:

![portable scanner](../main/media/portable_3D_scanner.jpg)

and build 3D point cloud models based on only these 240 images. 

![3D point cloud models](../main/media/bean_root.png)


    
# Installation

The easiest way to use this software is with Docker or Singularity. A public Docker image definition is available: `computationalplantscience/3d_colmap`

## Docker

Pull an image or a repository from a registry
```shell
docker pull computationalplantscience/3d_colmap
```
Mount the current working directory "/opt/dev" and open an interactive shell:

```shell
docker run -it -v $(pwd):/opt/dev -w /opt/dev computationalplantscience/3d_colmap bash
```

This docker container was compiled based on nvidia/cuda:12.2.2-devel-ubuntu22.04, and supports GPU running under HPC Singularity environment. This docker was tested on GPU node in Puma HPC. 

It will automatically detect the CPU and GPU architectures, if GPU was detected, it will use CUDA to speed up. 

COLMAP_VERSION=3.9

CUDA_ARCHITECTURES=70

The Docker recipe file was in "Dockerfile", and DockerHub (computationalplantscience/3d_colmap) was setup linked to this repo directly and in automatic trigger compile mode.
 
The Colmap pipeline was in bash file "colmap_pipeline.sh"





## Singularity

Open a shell in your current working directory:

```shell
singularity shell docker://computationalplantscience/3d_colmap
```



# Usage

## Reconstructing a 3D point cloud

To reconstruct a point cloud from an image set, use `colmap_pipeline.sh` as such:

```shell
    ./colmap_pipeline.sh
```

A successful reconstruction will produce several files in the output directory:

- `sparse.ply`: sparse point cloud model
- `dense.ply`: dense point cloud model



#### Colmap configuration

There are several configurable values for colmap's patch matching step during dense reconstruction. Optimal values will vary by host machine.

- `--cache_size`: cache size (in GB) to use during patch matching, defaults to `32`
- `--window_step`: patch window step size, defaults to `1`
- `--window_radius`: patch window radius, defaults to `5`
- `--num_iterations`: number of patch match iterations, defaults to `5`
- `--num_samples`: number of sampled views, defaults to `15`
- `--geom_consistency`: whether to perform geometric dense reconstruction, defaults to `True`

## Visualizing a 3D point cloud

Currently this software does not support model visualization. PLY files can be visualized with e.g. [Meshlab](https://www.meshlab.net/) or [cloudcompare](https://www.danielgm.net/cc/).

# Dependencies

This software is built on top of COLMAP, Recommended dependencies: CUDA (at least version 7.X).



### COLMAP
https://colmap.github.io
Author: Johannes L. Schoenberger (jsch-at-demuc-dot-de)
@inproceedings{schoenberger2016sfm,
    author={Sch\"{o}nberger, Johannes Lutz and Frahm, Jan-Michael},
    title={Structure-from-Motion Revisited},
    booktitle={Conference on Computer Vision and Pattern Recognition (CVPR)},
    year={2016},
}

@inproceedings{schoenberger2016mvs,
    author={Sch\"{o}nberger, Johannes Lutz and Zheng, Enliang and Pollefeys, Marc and Frahm, Jan-Michael},
    title={Pixelwise View Selection for Unstructured Multi-View Stereo},
    booktitle={European Conference on Computer Vision (ECCV)},
    year={2016},
}

# Author
Suxing Liu (suxingliu@gmail.com)

## Other contributions

Docker container was maintained and deployed to [PlantIT](https://portnoy.cyverse.org) by Wes Bonelli (wbonelli@uga.edu).

# License
GNU Public License

# Docker recipe 

This docker recipe was developed based on COLMAP official documents:

https://github.com/colmap/colmap/tree/main/docker  


# Note: 
This repo was to replace the old one "Computational-Plant-Science/3D_model_reconstruction_demo" which has compatible issue after HPC Puma upgraded to new OS sysytem. 
