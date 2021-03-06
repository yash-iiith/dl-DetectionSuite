# DeepLearningSuite
DeepLearning Suite is a set of tool that simplify the evaluation of most common object detection datasets with several object detection neural networks.

The idea is to offer a generic infrastructure to evaluates object detection algorithms againts a dataset and compute most common statistics:
* Intersecion Over Union
* Precision
* Recall 



##### Supported datasets formats:
* YOLO
* Jderobot recorder logs
* Princeton RGB dataset [1]
* Spinello dataset [2]

##### Supported object detection frameworks/algorithms
* YOLO (darknet)
* Background substraction



# Sample generation Tool
Sample Generation Tool has been developed in order to simply the process of generation samples for datasets focused on object detection. The tools provides some features to reduce the time on labeling objects as rectangles. 


# Requirements

### CUDA
```
  # NVIDIA_GPGKEY_SUM=d1be581509378368edeec8c1eb2958702feedf3bc3d17011adbf24efacce4ab5 && \
     NVIDIA_GPGKEY_FPR=ae09fe4bbd223a84b2ccfce3f60f4b3d7fa2af80 && \
     apt-key adv --fetch-keys http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/7fa2af80.pub && \
     apt-key adv --export --no-emit-version -a $NVIDIA_GPGKEY_FPR | tail -n +5 > cudasign.pub && \
     echo "$NVIDIA_GPGKEY_SUM  cudasign.pub" | sha256sum -c --strict - && rm cudasign.pub && \
     echo "deb http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64 /" > /etc/apt/sources.list.d/cuda.list && \
     echo "deb http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1604/x86_64 /" > /etc/apt/sources.list.d/nvidia-ml.list
 
 # apt-get install -y cuda
```

### Common deps
```
 # apt-get install -y build-essential git cmake rapidjson-dev libboost-dev sudo
```

### Opencv
```
    # apt-get install libopencv-dev 
```

### JDEROBOT
#### Deps
``` 
    # apt-get install -y libboost-filesystem-dev libboost-system-dev libboost-thread-dev libeigen3-dev libgoogle-glog-dev \
          libgsl-dev libgtkgl2.0-dev libgtkmm-2.4-dev libglademm-2.4-dev libgnomecanvas2-dev libgoocanvasmm-2.0-dev libgnomecanvasmm-2.6-dev \
          libgtkglextmm-x11-1.2-dev libyaml-cpp-dev icestorm zeroc-ice libxml++2.6-dev qt5-default libqt5svg5-dev libtinyxml-dev \
          catkin libssl-dev
```

#### Jderobot ThirdParty libraries:
```
    git clone https://github.com/JdeRobot/ThirdParty 
    cd ThirdParty
    cd qflightinstruments 
    qmake  qfi.pro
    make -j4
    make install

```

#### Jderobot

```
    git clone https://github.com/JdeRobot/JdeRobot
    cd JdeRobot 
    cmake . -DENABLE_ROS=OFF 
    make -j4 
    cmake . 
    sudo make install
```

### Darknet (jderobot fork)
```
    git clone https://github.com/JdeRobot/darknet && \
    cd darknet && \
    cmake . -DCMAKE_INSTALL_PREFIX=<DARKNET_DIR> && \
    make -j4 && \
    sudo make -j4 install && \
    cmake . && \
    rm -rf * && \
    cmake . -DCMAKE_INSTALL_PREFIX=$DARKNET_DIR && \
    make -j4 && \
    sudo make -j4 install
```
Change <DARKNET_DIR> to your custom installation path.

# How to compile DL_DetectionSuite:
Once you have all the deps installed just:
```
    git clone https://github.com/JdeRobot/DeepLearningSuite 
    cd DeepLearningSuite 
    cd DeepLearningSuite/ 
    cmake . -DDARKNET_PATH=<DARKNET_DIR>
```

# References.
[1] http://tracking.cs.princeton.edu/dataset.html \
[2] http://www2.informatik.uni-freiburg.de/~spinello/RGBD-dataset.html \
[3] YOLO: https://pjreddie.com/darknet/yolo/ \
[4] YOLO with c++ API: https://github.com/jderobot/darknet
