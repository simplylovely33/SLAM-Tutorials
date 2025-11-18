# SLAM-Tutorials
This is a tutorial for learning SLAM.

## Knowledge
Clarify the definition of technical terms:

***Camera Pose*** generally represents the camera positon and orientation relative to the world coordinate system.

***T_wc***(*world-to-camera*) indicates transform point in the world coordinate system into the camera coordiante system, which is used for projecting the world points into the camera image such as **rendering** and **reprojection**.

***T_cw***(*camera-to-world*) depicts transform point in the camera coordinate system into the world coordiante system, which is used for describing the camera position in the world such as camera trajectory **evalutaion** and **visualization**.

## Perception
### 1. Feature Extraction



### 2. Depth Estimation



## Evaluation
We using the prevalent package as [evo](https://github.com/MichaelGrupp/evo) for evaluating the camera trajectory, which support for different kinds of trajectory formats such as **TUM**, **KITTI**, elaborate format information refer to [here](https://github.com/MichaelGrupp/evo/wiki/Formats).

### `kitti` pose format
Below is the pose formate of **KITTI** dataset, which has **no timestamps** so you need to be severly careful when you compare two files because the length of two poses must be the same.

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
Below is the pose formate of **TUM** RGB-D dataset. Each row has timestamp, camera position and orientation(as quaternion)  with each value is seperated by a space.

Pose sequence looks like:
```
timestamp x y z q_x q_y q_z q_w
```

