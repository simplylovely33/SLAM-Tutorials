# SLAM-Tutorials
This is a tutorial for learning SLAM.

## Perception
### 1. Feature Extraction

### 2. Depth Estimation

## Evaluation
Clear the definition of world-to-camera(T_wc) and camera-to-world(T_cw) transform. Both of them are the 4x4 homogeneous transformation matrix.

*T_wc* indicates transform point in *world* into the *camera* coordiante system, which is used for rendering and reprojection loss calculation.

*T_cw* depicts transform point in *camera* into the *world* coordiante system, which is used for describe the camera position in the world.
