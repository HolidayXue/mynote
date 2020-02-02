python setup_win_gpu.py build_ext --inplace


Getting the nvcc fatal   : '--ptxas-options=-v': expected a number error when I try to build a Windows port of Faster-RCNN. You may reach the setup file (which is a Python script) directly from here.

Software Environment:

- CUDA v10.1
- VS 2019
- Python 3.7
- Windows 10



This configuration line is no longer correct with CUDA 10.1:

nvcc_compile_args = ['-O', '--ptxas-options=-v', '-arch=sm_35', '-c', '--compiler-options=-fPIC']
That will generate a nvcc compile command that looks like this:

nvcc -O ...
With CUDA 10.0 and prior, such a command was legal. With CUDA 10.1 it is not. This switch passes the optimization level for host code, so barring any reason not to, I would recommend passing -O3 here:

nvcc_compile_args = ['-O3', '--ptxas-options=-v', '-arch=sm_35', '-c', '--compiler-options=-fPIC']



使用命令 python setup_win_gpu.py build_ext --inplace进行安装
若出现
gpu_nms.cpp(2190): error C2664: “void _nms(int *,int *,const float *,int,int,float,int)”: 无法将参数 1 从“__pyx_t_5numpy_int32_t *”转换为“int *”
gpu_nms.cpp(2190): note: 与指向的类型无关；强制转换要求 reinterpret_cast、C 样式强制转换或函数样式强制转换
error: command 'C:\\Program Files\\NVIDIA GPU Computing Toolkit\\CUDA\\v10.1\\bin\\nvcc.exe' failed with exit status 2
则将__pyx_t_5numpy_int32_t 替换为int
gpu_nms.cpp(2162): error C2664: “void _nms(int *,int *,const float *,int,int,float,int)”: 无法将参数 1 从“__pyx_t_5numpy_int32_t *”转换为“int *”
gpu_nms.cpp(2162): note: 与指向的类型无关；强制转换要求 reinterpret_cast、C 样式强制转换或函数样式强制转换
error: command 'C:\\Program Files\\NVIDIA GPU Computing Toolkit\\CUDA\\v10.1\\bin\\nvcc.exe' failed with exit status 2


将2162行的 __pyx_t_5numpy_int32_t *修改为int *
