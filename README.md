# SLAM-Tutorials
This is a tutorial for learning SLAM.

## Knowledge
Clarify the definition of technical terms:

***Point Cloud*** is a set of points that represents the 3D shape or object. Each point is associated with 3D position (***x, y, z***) and sometimes with additional information such as color (***R, G, B***), intensity, or normal vector.

***Camera Pose*** generally represents the camera positon and orientation relative to the world coordinate system.

***T_wc***(*world-to-camera*) indicates transform point in the world coordinate system into the camera coordiante system, which is used for projecting the world points into the camera image such as **rendering** and **reprojection**.

***T_cw***(*camera-to-world*) depicts transform point in the camera coordinate system into the world coordiante system, which is used for describing the camera position in the world such as camera trajectory **evalutaion** and **visualization**.

## Perception
There are multiple visual SLAM with different perception frontiers, such as **Monocular**, **Stereo**, **RGB-D**, **LiDAR** etc. The purpose of perception is extract the image feature, estimate the camera pose and reconstruct the 3D environment.

### 1. Feature Extraction
This conventional feature extraction phase is consist of feature detection and matching. First, we need to adopt the `detector` to gain the keypoint positions from image and utilize the `matcher` to generate descriptors that comprise of local information for each keypoint. Then, based on calculating the distance between two feature descriptors, we can regard the lowest distance as the highest similarity to establish the potential correspoence. Furthermore, there are still exist the inaccurate matching results among the initial matches. We can use `filter` to remove incorrect sample and deliver the final matches

|Method|Harris|SIFT|SURF|FAST|BRIEF|ORB|
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| *detector* | ✓ | ✓ | ✓ | ✓ | – | ✓ |
| *matcher* | – | ✓ | ✓ | – | ✓ | ✓ |


|Type|SP+SG|R2D2|LoFTR|Silk|LightGlue|ELoFTR|EDM|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| *w*. *detector* | ✓ | ✓ | – | ✓ | – | – | – |
| *w*.*o*. *detector* | – | – | ✓ | – | ✓ | ✓ | ✓ |

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

