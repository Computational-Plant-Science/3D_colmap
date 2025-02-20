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


    
# Note: 

This repo was to replace the old one "Computational-Plant-Science/3D_model_reconstruction_demo" which has compatible issue after HPC Puma upgraded to new OS sysytem. 
