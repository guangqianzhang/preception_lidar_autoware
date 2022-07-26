autoware from jzl
there some changes for an advanced OpenCV
1. for CV_AA. we add "#define CV_AA cv::LINE_AA"
2. for CV_FILLED . we add "define CV_FILLED cv::FILLED"
3. delete the line in diar_euclidean_cluster_detect.cpp #include <opencv2/contrib.contrib.hpp>
4. for param_k and param_radius . we change it to *param_k in kdtree_flann.h
5. add #include "gencolors.cpp" out CV_MAJOR_VERSION==3
