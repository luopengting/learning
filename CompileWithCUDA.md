## Failed to parse CUDA nvcc implicit link information
```
CMake Error at /usr/share/cmake-3.16/Modules/CMakeDetermineCUDACompiler.cmake:187 (message):
    Failed to extract nvcc implicit link line.


Failed to parse CUDA nvcc implicit link information:
    no "PATH=" string found in "nvcc" output:
Failed to parse CUDA nvcc implicit link information:
    no "LIBRARIES=" string found in "nvcc" output:
```
### solution
Add in CMakeLists.txt:
```
set(CMAKE_CUDA_COMPILER /usr/local/cuda-11.6/bin/nvcc)
find_package(CUDAToolkit)
```

## CUDA_STANDARD is set to invalid value '17'
When we use `set(CMAKE_CUDA_STANDARD 17)` in CMakeLists and error occurs:
```
CUDA_STANDARD is set to invalid value '17'
```
Upgrade the cmake, the cmake installed by 'apt-get install' is old, upgrade it to `3.22.4` or later and the problem will be solved.

## undefined symbol
```
ImportError: /home1/miniconda3/envs/dpvo/lib/python3.10/site-packages/dpviewerx.cpython-310-x86_64-linux-gnu.so: undefined symbol: _ZN8pangolin7DisplayERKSs
```
### check
```
readelf -d /home1/miniconda3/envs/dpvo/lib/python3.10/site-packages/dpviewerx.cpython-310-x86_64-linux-gnu.so
```
![image](https://github.com/luopengting/learning/assets/22173722/7865da94-25ed-4162-a2c3-83a4dba359a5)
```
c++filt _ZN8pangolin7DisplayERKSs
nm -gDC /usr/local/lib/libpango_display.so | grep -i Display
```
![image](https://github.com/luopengting/learning/assets/22173722/9a3e88d8-5339-4d53-baf5-fa88d070ce58)

### solution
add compile definition in Pangolin CMakeLists.txt
```
add_compile_definitions(_GLIBCXX_USE_CXX11_ABI=0)
```
