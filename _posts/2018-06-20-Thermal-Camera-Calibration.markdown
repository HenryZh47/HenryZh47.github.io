---
title:  "Methods of thermal camera calibration"
date:   2018-06-20 17:20:17 -0400
toc: true
toc_sticky: true
---
This is a brief overview of a research paper that I did during Summer 2018 with my classmate Ruixuan Liu (https://github.com/waynekyrie). The pdf version can be downloaded at the end of this post.

## Introduction
Geometric calibration is required in existing monocular and multi-view geometry-based computer vision algorithms and applications. Due to the manufacturing process, distortion is introduced to the cameras, making objects appear distorted on the image. Lens distortion increases as the pixel approach to the border of the image. Such optic distortion leads to inaccurate transformation map between 3-dimensional object points and 2-dimensional image points. In the geometry-based vision, an accurate 3D to 2D mapping is required. Therefore, geometric calibration is a crucial step that directly influences the accuracy and performance of algorithms and applications.

We introduce three different calibration targets that provide heat pattern for thermal cameras. With these targets, Zhang's algorithm, implemented in OpenCV toolkit, can be performed with thermal cameras. In addition, we propose a template matching method to extract the thermal feature points as the prerequisite for using the existing OpenCV calibration toolkit. We then compare the MRE(Mean Re-projection Error) from each calibration target along with the MRE from visual camera calibration with conventional chessboard target to evaluate the quality of the calibration. The proposed calibration methods make the thermal calibration process more convenient and feasible, as well as provide high-quality and accurate thermal geometric calibration results.

## Temperature pattern generation methods
### Nichrome wire method
We use nickle-chromium heat resisting wire as thermal source and a 24*24 inch acrylic board as baseboard. Then hook it up with a 30V/5A power source. The wire will heat up under the current and become visible to the thermal camera.

Designed and fabricated the following setup:
<figure class="half">
  <a href="/assets/images/thermal_calibration/hotwire_front.jpeg"><img src="/assets/images/thermal_calibration/hotwire_front.jpeg"></a>
  <a href="/assets/images/sthermal_calibration/hotwire_back.jpeg"><img src="/assets/images/thermal_calibration/hotwire_back.jpeg"></a>
  <figcaption>nickle-chrominum hardware setup</figcaption>
</figure>

<figure>
  <a href="/assets/images/thermal_calibration/thermal_img/20180524_161845.jpg"><img src="/assets/images/thermal_calibration/thermal_img/20180524_161845.jpg"></a>
  <figcaption> Thermal image of the calibration target </figcaption>
</figure>

### Foam metal-plate method
This method generates temperature pattern by inserting cold aluminum disks into foam board. It uses asymmetric circle calibration pattern for easy machining. The aluminum disks are painted to black so that the pattern is also recognizable to RGB cameras, making it feasible to calibrate the extrinsic parameters between thermal and RGB cameras.

<figure>
  <a href="/assets/images/thermal_calibration/foam_setup.jpeg"><img src="/assets/images/thermal_calibration/foam_setup.jpeg"></a>
  <figcaption> Foam metal-plate hardware setup </figcaption>
</figure>

<figure>
  <a href="/assets/images/thermal_calibration/foam_thermal.jpg"><img src="/assets/images/thermal_calibration/foam_thermal.jpg"></a>
  <figcaption> Thermal image of the foam metal-plate setup </figcaption>
</figure>

Thanks to Joseph Bartels who designed the calibration board and Chuck Whittaker who fabricated the device.

### Light heating checkerboard method
This method utilizes the property that the black part of the checkerboard would absorb more heat from light and thus make the temperature of the black blocks higher than that of white blocks. Different light source can lead to different quality calibrations. Even distribution of light is considered good. We experimented with both a lamp and sunlight as light sources.

<figure>
  <a href="/assets/images/thermal_calibration/direct_setup.jpeg"><img src="/assets/images/thermal_calibration/direct_setup.jpeg"></a>
  <figcaption> Light heating hardware setup </figcaption>
</figure>

<figure>
  <a href="/assets/images/thermal_calibration/direct_thermal.jpeg"><img src="/assets/images/thermal_calibration/direct_thermal.jpeg"></a>
  <figcaption> Thermal image of the foam metal-plate setup </figcaption>
</figure>


## Template matching to find feature points
Since the thermal images are not as sharp as RGB images, we use the following template matching method to extract feature points that will be used in the future calibration.

The main idea behind the template matching method is to first manually extract template that has the feature in it, then traverse the template through the entire image to find the windows that have highest similarities with the template. This method fits the situation where features cannot be tracked by nice lines because of the blurred lines in thermal images. Below is a procedure chart of the method:

<figure>
  <a href="/assets/images/thermal_calibration/flow_chart.png"><img src="/assets/images/thermal_calibration/flow_chart.png"></a>
  <figcaption> Template matching procedures </figcaption>
</figure>

<figure class="half">
  <a href="/assets/images/sthermal_calibration/chess_draw.jpg"><img src="/assets/images/thermal_calibration/chess_draw.jpg"></a>
  <a href="/assets/images/thermal_calibration/chess.jpg"><img src="/assets/images/thermal_calibration/chess.jpg"></a>
  <figcaption>Found features and arrange in order</figcaption>
</figure>

<figure class="half">
  <a href="/assets/images/sthermal_calibration/chess_original.jpg"><img src="/assets/images/thermal_calibration/chess_original.jpg"></a>
  <a href="/assets/images/thermal_calibration/chess_distorted.jpg"><img src="/assets/images/thermal_calibration/chess_distorted.jpg"></a>
  <figcaption>Original and undistorted image</figcaption>
</figure>


## Credits
Ruixuan Liu (Template matching method): https://github.com/waynekyrie
Zhengyou Zhang (A New Technique for Camera Calibration) :https://www.microsoft.com/en-us/research/wp-content/uploads/2016/02/tr98-71.pdf

## PDF version
<embed width="100%" height="100%" name="plugin" id="plugin" src="https://henryzh47.github.io/assets/documents/multiple-methods-geometric.pdf" type="application/pdf" internalinstanceid="3">
