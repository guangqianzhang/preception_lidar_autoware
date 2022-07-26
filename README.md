# preception_lidar_autoware
preception_lidar_autoware


autoware from jzl there some changes for an advanced OpenCV

    for CV_AA. we add "#define CV_AA cv::LINE_AA"
    for CV_FILLED . we add "define CV_FILLED cv::FILLED"
    delete the line in diar_euclidean_cluster_detect.cpp #include <opencv2/contrib.contrib.hpp>
    for param_k and param_radius . we change it to *param_k in kdtree_flann.h
    add #include "gencolors.cpp" out CV_MAJOR_VERSION==3

