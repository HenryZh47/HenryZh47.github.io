---
title:  "Reconstruction Sensor Pod Project"
date:   2018-08-10 02:18:17 -0400
header:
  overlay_image: /assets/images/sensor_pod_photos/isometric_header.jpg
  overlay_filter: 0.25
  caption: 3D Reconstruction Sensor Pod
toc: true
toc_sticky: true
---

This is a project that I've been working on during my internship at the Airlab since May 2018. The goal of this sensor pod is to achieve high accuracy 3D reconstruction using a pair of high resolution XIMEA stereo cameras and a Velodyne LiDAR. The device can also provide thermal information using the onboard FLIR thermal camera.

## Hardware Overview
<figure>
  <a href="/assets/images/sensor_pod_photos/front_description.jpg"><img src="/assets/images/sensor_pod_photos/front_description.jpg"></a>
  <figcaption> Hardware overview of the sensor pod</figcaption>
</figure>

As shown in the picture, the sensor pod consists of a set of sensors (stereo/thermal cameras, LiDAR, IMU), an Intel NUC onboard computer, a DJI battery as power supply, and other components (two voltage converters, two USB hubs, and a teensy for sensor triggering).

All the sensors are mounted on a single aluminum sheet to ensure no undesired displacement will happen between sensors when operating. The device can be used both hand-held or mounted on a tripod.
<figure class="half">
  <a href="/assets/images/sensor_pod_photos/tripod.jpeg"><img src="/assets/images/sensor_pod_photos/tripod.jpeg"></a>
  <a href="/assets/images/sensor_pod_photos/hand_held.jpg"><img src="/assets/images/sensor_pod_photos/hand_held.jpg"></a>
  <figcaption>Hand-held and tripod configuration</figcaption>
</figure>

The Velodyne LiDAR is connected to a g2 customized motor, allowing the LiDAR to externally rotate. Combining the encoder data from the motor and the Velodyne sensor data points, we can generate a denser point cloud that covers the entire 3D space.

<figure class="half">
  <a href="/assets/images/sensor_pod_photos/corridor1.png"><img src="/assets/images/sensor_pod_photos/corridor1.png"></a>
  <a href="/assets/images/sensor_pod_photos/outside1.png"><img src="/assets/images/sensor_pod_photos/outside1.png"></a>
  <figcaption>Velodyne LiDAR data points visualization</figcaption>
</figure>

<iframe width="560" height="315" src="https://www.youtube.com/embed/0I8w8B87FbY" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

## Algorithms Overview
With the stereo images as data, we can find corresponding feature points in both images and construct the disparity map for a pair of images. Combining the disparity map and the camera parameters (both intrinsic and extrinsic parameters), we can compute the depth map of the target, and then construct the point cloud from the feature points.

We can then produce the mesh from the point clouds, and then put image and thermal texture onto the mesh as the result.

## Results
Here are some results for now:

<figure>
  <a href="/assets/images/sensor_pod_photos/result3.png"><img src="/assets/images/sensor_pod_photos/result3.png"></a>
  <figcaption> Reconstructed mesh with visual and thermal texture </figcaption>
</figure>

<figure>
  <a href="/assets/images/sensor_pod_photos/result1.png"><img src="/assets/images/sensor_pod_photos/result1.png"></a>
  <figcaption> Reconstructed mesh of two consecutive shots (front) </figcaption>
</figure>

<figure>
  <a href="/assets/images/sensor_pod_photos/result2.png"><img src="/assets/images/sensor_pod_photos/result2.png"></a>
  <figcaption> Reconstructed mesh of two consecutive shots (side) </figcaption>
</figure>



## Credit
Stereo vision algorithms: Yaoyu Hu, http://www.huyaoyu.com/
Thermal texture generation: Ruixuan Liu, https://github.com/waynekyrie
