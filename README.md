# MHFormer: Multi-Hypothesis Transformer for 3D Human Pose Estimation [CVPR 2022]

<p align="center"><img src="figure/pipline.jpg" width="100%" alt="" /></p>

> [**MHFormer: Multi-Hypothesis Transformer for 3D Human Pose Estimation**](https://arxiv.org/pdf/2111.12707),            
> Wenhao Li, Hong Liu, Hao Tang, Pichao Wang, Luc Van Gool,        
> *In IEEE Conference on Computer Vision and Pattern Recognition (CVPR), 2022*

<p float="left">
  <img src="figure/skating.gif" width="49%" />
  <img src="figure/anime.gif" width="49%" />


## Updates
- 05/12/2022: The pretrained models of 81-frames, 243-frames, 351-frames are released!
- 03/24/2022: Demo and in-the-wild inference code is released! 

## Installation

- Create a conda environment: ```conda create -n mhformer python=3.7```
- Download cudatoolkit=11.0 from [here](https://developer.nvidia.com/cuda-11.0-download-archive) and install 
- ```pip3 install torch==1.7.1+cu110 torchvision==0.8.2+cu110 -f https://download.pytorch.org/whl/torch_stable.html```
- ```pip3 install -r requirements.txt```
  
## Dataset setup

Please download the dataset from [Human3.6M](http://vision.imar.ro/human3.6m/) website and refer to [VideoPose3D](https://github.com/facebookresearch/VideoPose3D) to set up the Human3.6M dataset ('./dataset' directory). 
Or you can download the processed data from [here](https://drive.google.com/drive/folders/112GPdRC9IEcwcJRyrLJeYw9_YV4wLdKC?usp=sharing). 

```bash
${POSE_ROOT}/
|-- dataset
|   |-- data_3d_h36m.npz
|   |-- data_2d_h36m_gt.npz
|   |-- data_2d_h36m_cpn_ft_h36m_dbb.npz
```

## Download pretrained model

The pretrained model can be found in [here](https://drive.google.com/drive/folders/1UWuaJ_nE19x2aM-Th221UpdhRPSCFwZa?usp=sharing), please download it and put it in the './checkpoint/pretrained' directory. 

## Test the model

To test on a 351-frames pretrained model on Human3.6M:

```bash
python main.py --test --previous_dir 'checkpoint/pretrained/351' --frames 351
```

Here, we compare our MHFormer with recent state-of-the-art methods on Human3.6M dataset. Evaluation metric is Mean Per Joint Position Error (MPJPE) in mm​. 


|   Models    |  MPJPE   |
| :---------: | :------: |
| VideoPose3D |   46.8   |
| PoseFormer  |   44.3   |
|  MHFormer   | **43.0** |


## Train the model

To train a 351-frames model on Human3.6M:

```bash
python main.py --framse 351 --batch_size 128
```

The batch size can be changed depending on your machine. 

## Demo
First, you need to download YOLOv3 and HRNet pretrained models [here](https://drive.google.com/drive/folders/1_ENAMOsPM7FXmdYRbkwbFHgzQq_B_NQA?usp=sharing) and put it in the './demo/lib/checkpoint' directory. 
Then, you need to put your in-the-wild videos in the './demo/video' directory. 

Run the command below:
```bash
python demo/vis.py --video sample_video.mp4
```

Sample demo output:

<p align="center"><img src="figure/sample_video.gif" width="60%" alt="" /></p>


## Order of Keypoints in Dataset and Model Predictions
3D prediction = 2D prediction = 2D keypoints in dataset
```
0 = between hips
1 = right hip
2 = right knee
3 = right ankle
4 = left hip
5 = left knee
6 = left ankle
7 = back
8 = neck
9 = head (lips)
10 = sitehead (forehead)
11 = left shoulder
12 = left elbow
13 = left wrist
14 = right shoulder
15 = right elbow
16 = right wrist
```
![](https://imgur.com/iKZPIsh.png)

3D keypoints in dataset
```
0 = between hips
1 = right hip
2 = right knee
3 = right ankle
6 = left hip
7 = left knee
8 = left ankle
12 = back
13 = neck
14 = head (lips)
15 = sitehead (forehead)
17 = left shoulder
18 = left elbow
19 = left wrist
25 = right shoulder
26 = right elbow
27 = right wrist
```
![](https://imgur.com/5pkuTwK.png)

## Citation

If you find our work useful in your research, please consider citing:

    @inproceedings{li2022mhformer,
      title={MHFormer: Multi-Hypothesis Transformer for 3D Human Pose Estimation},
      author={Li, Wenhao and Liu, Hong and Tang, Hao and Wang, Pichao and Van Gool, Luc},
      booktitle={Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition (CVPR)},
      year={2022}
    }

## Acknowledgement

Our code is extended from the following repositories. We thank the authors for releasing the codes. 

- [ST-GCN](https://github.com/vanoracai/Exploiting-Spatial-temporal-Relationships-for-3D-Pose-Estimation-via-Graph-Convolutional-Networks)
- [VideoPose3D](https://github.com/facebookresearch/VideoPose3D)
- [3d-pose-baseline](https://github.com/una-dinosauria/3d-pose-baseline)
- [3d_pose_baseline_pytorch](https://github.com/weigq/3d_pose_baseline_pytorch)
- [StridedTransformer-Pose3D](https://github.com/Vegetebird/StridedTransformer-Pose3D)
## Licence

This project is licensed under the terms of the MIT license.
