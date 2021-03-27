# Neural Network CUDA Example
![logo](./image/logo.png)

A simple example for neural network toolkits (PyTorch, TensorFlow, etc.) calling custom CUDA operators.

We provide several ways to compile the CUDA kernels and their cpp wrapper, including jit, setuptools and cmake.

We also provide several python codes to call the CUDA kernels, including kernel time statistics and model training.

## Environments
* NVIDIA Driver: 418.116.00
* CUDA: 11.0
* Python: 3.7.3
* PyTorch: 1.7.0+cu110
* TensorFlow: 2.4.1
* CMake: 3.16.3
* Ninja: 1.10.0
* GCC: 8.3.0

*Cannot ensure successful running in other environments.*

## Code structure
```shell
├── include
│   └── add2.h # header file of add2 cuda kernel
├── kernel
│   └── add2_kernel.cu # add2 cuda kernel
├── pytorch
│   ├── add2_ops.cpp # torch wrapper of add2 cuda kernel
│   ├── time.py # time comparison of cuda kernel and torch
│   ├── train.py # training using custom cuda kernel
│   ├── setup.py
│   └── CMakeLists.txt
├── tensorflow
│   ├── add2_ops.cpp # tensorflow wrapper of add2 cuda kernel
│   ├── time.py # time comparison of cuda kernel and tensorflow
│   ├── train.py # training using custom cuda kernel
│   └── CMakeLists.txt
├── LICENSE
└── README.md
```

## PyTorch
### Compile cpp and cuda
**JIT**  
Directly run the python code.

**Setuptools**  
```shell
python3 setup.py install
```

**CMake**  
```shell
mkdir build
cd build
cmake -DCMAKE_PREFIX_PATH="$(python3 -c 'import torch.utils; print(torch.utils.cmake_prefix_path)')" ../pytorch
make
```

### Run python
**Compare kernel running time**  
```shell
python3 pytorch/time.py --compiler jit
python3 pytorch/time.py --compiler setup
python3 pytorch/time.py --compiler cmake
```

**Train model**  
```shell
python3 pytorch/train.py --compiler jit
python3 pytorch/train.py --compiler setup
python3 pytorch/train.py --compiler cmake
```

## TensorFlow
### Compile cpp and cuda
**CMake**  
```shell
mkdir build
cd build
cmake  ../tensorflow
make
```

### Run python
**Compare kernel running time**  
```shell
python3 tensorflow/time.py --compiler cmake
```

**Train model**  
```shell
python3 tensorflow/train.py --compiler cmake
```

## Implementation details (in Chinese)
[PyTorch自定义CUDA算子教程与运行时间分析](https://godweiyang.com/2021/03/18/torch-cpp-cuda)  
[详解PyTorch编译并调用自定义CUDA算子的三种方式](https://godweiyang.com/2021/03/18/torch-cpp-cuda-2)  
[三分钟教你如何PyTorch自定义反向传播](https://godweiyang.com/2021/03/18/torch-cpp-cuda-3)

## F.A.Q
Coming soon...