# SLAM-Tutorials
This is a tutorial for learning SLAM.

## Knowledge
Clarify the definition of technical terms:

***Point Cloud*** is a set of points that represents the 3D shape or object. Each point is associated with 3D position (***x, y, z***) and sometimes with additional information such as color (***R, G, B***), intensity, or normal vector.

***Camera Pose*** generally represents the camera position and orientation relative to the world coordinate system.

***T_wc***(*world-to-camera*) indicates transform point in the world coordinate system into the camera coordiante system, which is used for projecting the world points into the camera image such as **rendering** and **reprojection**.

***T_cw***(*camera-to-world*) depicts transform point in the camera coordinate system into the world coordiante system, which is used for describing the camera position in the world such as camera trajectory **evalutaion** and **visualization**.

## Perception
There are multiple visual SLAM with different perception frontiers, such as **Monocular**, **Stereo**, **RGB-D**, **LiDAR** etc. The purpose of perception is extract the image feature, estimate the camera pose and reconstruct the 3D environment.

### 1. Feature Extraction
This conventional feature extraction phase is consist of feature detection and matching. First, we need to adopt the `detector` to gain the keypoint positions from image and utilize the `matcher` to generate descriptors that comprise of local information for each keypoint. Then, based on calculating the distance between two feature descriptors, we can regard the lowest distance as the highest similarity to establish the potential correspoence. Furthermore, there are still exist the inaccurate matching results among the initial matches. We can use `filter` to remove incorrect sample and deliver the final matches.

Traditional hand-crafted method:
|Method|[Harris](https://www.bmva-archive.org.uk/bmvc/1988/avc-88-023.pdf)|[SIFT](https://www.cs.ubc.ca/~lsigal/425_2024W1/ijcv04.pdf)|[SURF](https://people.ee.ethz.ch/~surf/eccv06.pdf)|[FAST](https://www.edwardrosten.com/work/rosten_2006_machine.pdf)|[BRIEF](https://www.cs.ubc.ca/~lowe/525/papers/calonder_eccv10.pdf)|[ORB](https://par.cse.nsysu.edu.tw/resource/paper/2016/161129/ORB-an%20efficient%20alternative%20to%20SIFT%20or%20SURF.pdf)|
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| *detector* | ✓ | ✓ | ✓ | ✓ | – | ✓ |
| *matcher* | – | ✓ | ✓ | – | ✓ | ✓ |

With the development of deep learning, many works start to combine the ***Convolutional Neural Network*** or ***Transformer*** architecture to accompolish the feature extraction task. Subsequently, producing two different research direction, detector-based and detetor-free matching paradigm. 

Learning-based method with or without detector:
|Type|[SP](https://openaccess.thecvf.com/content_cvpr_2018_workshops/papers/w9/DeTone_SuperPoint_Self-Supervised_Interest_CVPR_2018_paper.pdf)+[SG](https://openaccess.thecvf.com/content_CVPR_2020/papers/Sarlin_SuperGlue_Learning_Feature_Matching_With_Graph_Neural_Networks_CVPR_2020_paper.pdf)|[R2D2](https://proceedings.neurips.cc/paper/2019/file/3198dfd0aef271d22f7bcddd6f12f5cb-Paper.pdf)|[LoFTR](https://openaccess.thecvf.com/content/CVPR2021/papers/Sun_LoFTR_Detector-Free_Local_Feature_Matching_With_Transformers_CVPR_2021_paper.pdf)|[SiLK](https://openaccess.thecvf.com/content/ICCV2023/papers/Gleize_SiLK_Simple_Learned_Keypoints_ICCV_2023_paper.pdf)|[LightGlue](https://openaccess.thecvf.com/content/ICCV2023/papers/Lindenberger_LightGlue_Local_Feature_Matching_at_Light_Speed_ICCV_2023_paper.pdf)|[ELoFTR](https://openaccess.thecvf.com/content/CVPR2024/papers/Wang_Efficient_LoFTR_Semi-Dense_Local_Feature_Matching_with_Sparse-Like_Speed_CVPR_2024_paper.pdf)|[EDM](https://arxiv.org/pdf/2503.05122)|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| *w*. *detector* | ✓ | ✓ | – | ✓ | ✓ | – | – |
| *w*.*o*. *detector* | – | – | ✓ | – | – | ✓ | ✓ |

### 2. Depth Estimation



## Evaluation
We using the prevalent package as [evo](https://github.com/MichaelGrupp/evo) for evaluating the camera trajectory, which support for different kinds of trajectory formats such as **TUM**, **KITTI** etc. Elaborate format information refer to [here](https://github.com/MichaelGrupp/evo/wiki/Formats).

### `kitti` pose format
Below is the pose format of **KITTI** dataset, which has **no timestamps** so we need to be severly careful when we compare two files because the length of two poses must be the same.

Each 4×4 homogeneous pose matrix is flattened into one sequence along the row direction, with each value is seperated by a space.

Pose matrix looks like:
```
a b c d
e f g h
i j k l
0 0 0 1
```
Flattened pose sequence looks like:
```
a b c d e f g h i j k l 0 0 0 1
```

### `tum` pose format
Below is the pose format of **TUM** RGB-D dataset. 

Each row has timestamp, camera position and orientation(as quaternion) with each value is seperated by a space.

Pose sequence looks like:
```
timestamp x y z q_x q_y q_z q_w
```

