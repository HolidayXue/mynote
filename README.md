# mynote

opencv 3.4 install (CentOS 7):

sudo yum -y update
sudo yum groupinstall 'Development Tools'
sudo yum install cmake git pkgconfig
sudo yum install libpng-devel libjpeg-turbo-devel jasper-devel openexr-devel libtiff-devel libwebp-devel
sudo yum install libdc1394-devel libv4l-devel gstreamer-plugins-base-devel
sudo yum install gtk2-devel
sudo yum install tbb-devel eigen3-devel

curl "https://bootstrap.pypa.io/get-pip.py" -o "get-pip.py"
sudo python get-pip.py

sudo yum install python-devel
sudo pip install numpy

cd opencv_path
mkdir build
cd build
cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D INSTALL_C_EXAMPLES=OFF -D INSTALL_PYTHON_EXAMPLES=OFF -D BUILD_EXAMPLES=OFF ..

CMAKE_INSTALL_PREFIX=/usr/local might need to be changed depends on where default python lib located

make -j $(nproc)
make install

if python lib does
ln -s /usr/local/lib/python2.7/site-packages/cv2.so cv2.so
