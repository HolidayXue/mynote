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