# A new contrast metric for the MSER detector

## Description
Feature detection and description algorithms are widely used for computer vision applications, such as SLAM, object detection, content-based image retrieval, etc.
For limited bandwidth applications (e.g. remote SLAM) a specific number of features can only be transmitted. Usually the features are selected according to their response value, which is a metric for the contrast. MSER [1] however, does not provide such a response value. In the paper we introduce a novel metric for the MSER detector to enable post-filtering of detected regions.

Oelsch et al. [2] evaluated the performance various feature extraction algorithms in a Mars-like environment. The authors found that MSER could benefit from a metric that can be used for post-filtering the detected regions. We use the same experimental setup with a location retrieval task using the Devon Island dataset [3]. In the following we provide a table of parameters we used during the region detection process. Note that the parameters for the method 'Manual' were selected in order to detect on average more than 1000 regions per image over the whole dataset. The parameter setting for 'All' detects more than 3000 regions on average per image. From this set of regions the contrast-based grid adapted methods select a subset of regions according to their contrast metric. DGA independently detects the appropriate number of regions by dynamic parameter adjustment as a wrapper around the MSER detector.

For MSER we used the OpenCV 3.3.0 implementation [5] and as descriptor we used OpenSURF [6].

## MSER Configuration
| Method  |    Parameters       |
| --------- | --------------------- |
|   Manual   | delta = 2<br>min_area = 36 <br> max_area = 12300 <br> max_variation = 0.25 |
|   All (relaxed param)     | delta = 1<br>min_area = 20 <br> max_area = 14400 <br> max_variation = 0.25 |
|   Random   | as above |
|   1_layer_MID_grid | as above |
|   BBox_MID_grid | as above |
| BBox_PD_grid [4] | as above |
| DGA_grid |  Initial parameters:<br> delta = 3 <br> min_area = 60 <br> max_area = 14400 <br> max_variation = 0.25 <br> <br> Configuration:<br> min_regions = 800 <br> max_regions = 1100 <br> no_iterations = 30 <br> <br> Interval ranges:<br> delta = [1, 5] <br> min_area = [16, 1000] <br> max_variation = [0.01, 5] |


## References
- [1] J. Matas, O. Chum, M. Urban, and T. Pajdla, “Robust wide-baseline stereo from maximally stable extremal regions,” Image and vision computing, vol. 22, no. 10, pp. 761–767, 2004.
- [2] M. Oelsch, D. V. Opdenbosch and E. Steinbach, "Survey of Visual Feature Extraction Algorithms in a Mars-like Environment," 2017 IEEE International Symposium on Multimedia (ISM), Taichung, 2017
- [3] [Devon Island Rover Navigation Dataset](http://asrl.utias.utoronto.ca/datasets/devon-island-rover-navigation/rover-traverse.html#Overview)
- [4] Y. Li, W. Jia, C. Shen and A. van den Hengel, "Characterness: An Indicator of Text in the Wild," in IEEE Transactions on Image Processing, vol. 23, no. 4, pp. 1666-1677, April 2014.
- [5] [Open Source Computer Vision Library](https://opencv.org)
- [6] C. Evans, "Notes on the opensurf library", University of Bristol, Tech. Rep., 2009
