# 3D_Point_Cloud_Registration_ICP

Implementation of 3D point cloud registration using the Iterative Closest Point (ICP) algorithm with visualization and quantitative error analysis.

---

## Introduction

In robotics, autonomous driving, and 3D computer vision, sensors such as LiDAR, depth cameras, and stereo vision systems generate large collections of 3D points known as **point clouds**. These point clouds represent the geometric structure of real-world environments.

However, point clouds captured from different viewpoints or time instants are typically misaligned due to sensor motion. To integrate multiple measurements into a consistent 3D representation, **point cloud registration** is required.

Point cloud registration estimates the optimal rigid transformation (rotation and translation) that aligns a source point cloud to a target point cloud. This process is fundamental in applications such as autonomous vehicle localization, SLAM (Simultaneous Localization and Mapping), 3D reconstruction, robotic navigation, and augmented reality.

This project implements and analyzes the **Iterative Closest Point (ICP)** algorithm for precise 3D point cloud registration.

---

## What is Point Cloud Registration?

Given two point clouds:

- Source point cloud Q  
- Target point cloud P  

the objective is to find a rigid transformation:

T = [ R  t  
      0  1 ]

where R is the rotation matrix and t is the translation vector, such that:

P ≈ RQ + t

The goal is to minimize the alignment error between corresponding points.

---

## What is ICP (Iterative Closest Point)?

Iterative Closest Point (ICP) is a classical optimization algorithm used for fine alignment of 3D point clouds.

### ICP Algorithm Workflow:

1. Initialize transformation  
2. Find closest point correspondences  
3. Estimate optimal rigid transformation  
4. Apply transformation  
5. Repeat until convergence  

At each iteration, ICP minimizes the squared Euclidean distance between corresponding points.

---

## Types of ICP Used

### 1. Point-to-Point ICP

Minimizes Euclidean distance between corresponding points.

Characteristics:
- Simple and robust  
- General-purpose alignment  
- Slower convergence  
- Lower accuracy on planar surfaces  

---

### 2. Point-to-Plane ICP

Minimizes distance along surface normals.

Characteristics:
- Faster convergence  
- Higher accuracy  
- Better performance on structured environments  
- Preferred for LiDAR-based mapping  

---

## Experimental Setup

The implementation uses the Open3D library to perform:

- Initial coarse alignment  
- Point-to-point ICP refinement  
- Point-to-plane ICP refinement  

Evaluation metrics:

- Fitness — proportion of inlier correspondences  
- Inlier RMSE — root mean squared error  
- Number of correspondences  

---

## Results and Analysis

Three stages of registration were performed and evaluated.

---

### 1. Initial Alignment (Coarse Registration)

Fitness = 0.1747  
Inlier RMSE = 0.01177  
Correspondences = 34,741  

Interpretation:
- Low fitness indicates poor initial alignment  
- Higher RMSE shows significant residual error  
- Provides a rough starting point for ICP  

---

### 2. Point-to-Point ICP

Fitness = 0.3724  
Inlier RMSE = 0.00776  
Correspondences = 74,056  

Estimated Transformation:

[[ 0.83924644  0.01006041 -0.54390867  0.64639961]  
 [-0.15102344  0.96521988 -0.21491604  0.75166079]  
 [ 0.52191123  0.26169520  0.81146378 -1.50303533]  
 [ 0.          0.          0.          1.        ]]

Interpretation:
- Fitness improves significantly  
- RMSE reduces  
- Number of correspondences more than doubles  
- Alignment quality improves substantially  

---

### 3. Point-to-Plane ICP

Fitness = 0.6209  
Inlier RMSE = 0.00658  
Correspondences = 123,471  

Estimated Transformation:

[[ 0.84023324  0.00618369 -0.54244126  0.64720943]  
 [-0.14752342  0.96523919 -0.21724508  0.81018928]  
 [ 0.52132423  0.26174429  0.81182576 -1.48366001]  
 [ 0.          0.          0.          1.        ]]

Interpretation:
- Highest fitness achieved  
- Lowest RMSE among all methods  
- Largest number of valid correspondences  
- Best alignment accuracy  

---

## Performance Comparison

| Method | Fitness ↑ | RMSE ↓ | Correspondences |
|----------|-------------|-----------|------------------|
| Initial Alignment | 0.1747 | 0.01177 | 34,741 |
| Point-to-Point ICP | 0.3724 | 0.00776 | 74,056 |
| Point-to-Plane ICP | 0.6209 | 0.00658 | 123,471 |

Conclusion:  
Point-to-plane ICP clearly outperforms point-to-point ICP in terms of alignment quality, accuracy, and convergence behavior.

---

## Reference

Tutorial followed:  
https://www.youtube.com/watch?v=3pjCWuTLLrQ  

The implementation was independently written, structured, and analyzed for deeper conceptual understanding.

