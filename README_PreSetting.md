# stereo_matching_cnn (ubuntu 16.04)

## 1. install torch (http://torch.ch/docs/getting-started.html)
### install ipython

* sudo apt-get update
* sudo apt-get upgrade

* sudo apt-get install python3-pip
* sudo pip3 install --upgrade pip

* sudo -H pip3 install ipython
* sudo -H pip3 install ipython --upgrade

### install jupyter

* sudo -H pip3 install jupyter
* sudo -H pip3 install jupyter --upgrade

### install torch

* sudo apt install git
* git clone https://github.com/torch/distro.git ~/torch --recursive
* cd ~/torch; bash install-deps;
* when "bash install-deps", if happen error "/sbin/ldconfig.real: /usr/lib/nvidia-375/libEGL.so.1 is not a symbolic link", 
solution is:
  - sudo mv /usr/lib/nvidia-375/libEGL.so.1 /usr/lib/nvidia-375/libEGL.so.1.org
  - sudo mv /usr/lib32/nvidia-375/libEGL.so.1 /usr/lib32/nvidia-375/libEGL.so.1.org
  - sudo ln -s /usr/lib/nvidia-375/libEGL.so.375.39 /usr/lib/nvidia-375/libEGL.so.1
  - sudo ln -s /usr/lib32/nvidia-375/libEGL.so.375.39 /usr/lib32/nvidia-375/libEGL.so.1
* ./install.sh
* source ~/.bashrc

### install itorch

* sudo apt-get install libzmq3-dev libssl-dev python3-zmq
* git clone https://github.com/facebook/iTorch.git
* cd iTorch/
* sudo env "PATH=$PATH" luarocks make
(ignore echo "Error: could not find ipython in PATH. Do you have it installed?")

* sudo chown -R $USER:$USER /home/$USER/.ipython
* sudo chown -R $USER $(dirname $(ipython locate profile))

### test

* itorch notebook

## 2. Install opencv-2.4.13 in Ubuntu 16.04
### install dependencies
* sudo apt-get update
* sudo apt-get install -y build-essential
* sudo apt-get install -y cmake
* sudo apt-get install -y libgtk2.0-dev
* sudo apt-get install -y pkg-config
* sudo apt-get install -y python-numpy python-dev
* sudo apt-get install -y libavcodec-dev libavformat-dev libswscale-dev
* sudo apt-get install -y libjpeg-dev libpng12-dev libtiff5-dev libjasper-dev
* sudo apt-get -qq install libopencv-dev build-essential checkinstall cmake pkg-config yasm libjpeg-dev libjasper-dev libavcodec-dev libavformat-dev libswscale-dev libdc1394-22-dev libxine2 libgstreamer0.10-dev libgstreamer-plugins-base0.10-dev libv4l-dev python-dev python-numpy libtbb-dev libqt4-dev libgtk2.0-dev libmp3lame-dev libopencore-amrnb-dev libopencore-amrwb-dev libtheora-dev libvorbis-dev libxvidcore-dev x264 v4l-utils
 
### download opencv-2.4.13
* wget http://downloads.sourceforge.net/project/opencvlibrary/opencv-unix/2.4.13/opencv-2.4.13.zip
* unzip opencv-2.4.13.zip
* cd opencv-2.4.13
* mkdir release
* cd release
 
### compile and install
* cmake -G "Unix Makefiles" -DCMAKE_CXX_COMPILER=/usr/bin/g++ CMAKE_C_COMPILER=/usr/bin/gcc -DCMAKE_BUILD_TYPE=RELEASE -DCMAKE_INSTALL_PREFIX=/usr/local -DWITH_TBB=ON -DBUILD_NEW_PYTHON_SUPPORT=ON -DWITH_V4L=ON -DINSTALL_C_EXAMPLES=ON -DINSTALL_PYTHON_EXAMPLES=ON -DBUILD_EXAMPLES=ON -DWITH_QT=ON -DWITH_OPENGL=ON -DBUILD_FAT_JAVA_LIB=ON -DINSTALL_TO_MANGLED_PATHS=ON -DINSTALL_CREATE_DISTRIB=ON -DINSTALL_TESTS=ON -DENABLE_FAST_MATH=ON -DWITH_IMAGEIO=ON -DBUILD_SHARED_LIBS=OFF -DWITH_GSTREAMER=ON ..
* make all -j2 # 2 cores
* sudo make install
 
### ignore libdc1394 error http://stackoverflow.com/questions/12689304/ctypes-error-libdc1394-error-failed-to-initialize-libdc1394
 
### Test
* #python
* #> import cv2
* #> cv2.SIFT
* #<built-in function SIFT>

## 3. install png++ (http://www.nongnu.org/pngpp/doc/0.2.9/)
### download : 
* http://download.savannah.nongnu.org/releases/pngpp/

### Unpack source package:
* $ tar -zxf png++-0.2.x.tar.gz -C ~/src 

### Go to your brand new png++ sources directory:
* $ cd ~/src/png++-0.2.x 

### Issue make to test how it's doing:
* $ make 
* This will compile examples in the example directory. If everything goes well, try
* $ make test 
* (or make check which is the same as above) to run the test suite. If tests do not produce error messages then probably all is OK.

### Now you can create documentation (optional). Use
* $ make docs 
* to run doxygen in the sources directory.

### Now it is time to become root and install png++ into your system. It's OK to issue make install under ordinary user permissions if you want to install png++ into your home directory. Run the following command:
* $ make install PREFIX=$HOME 
* to copy png++ header files to ~/include/png++ and documentation files to ~/share/doc/png++-0.2.x. Without a PREFIX png++ installs to /usr/local.
  - sudo make install
