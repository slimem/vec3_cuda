# vec3_cuda
A small and fast header only class for 3D vectors computation using Cuda.

---
## Usage
This class can be used by both ```__host__``` and ```__device__```.
Please note that the file is compiled twice, once for the host and once for the device. The latter sets the macro ```__CUDA_ARCH__``` which will make the class use Cuda intrinsics instead of plain computations:
```cpp
#ifdef __CUDA_ARCH__
#define USE_INTRINSICS
#endif
```
On the *host*, a vec3 dot product is computed like the following:
```cpp
__host__ static constexpr float dot(const vec3& v1, const vec3& v2) {
        return v1._v[0] * v2._v[0] + v1._v[1] * v2._v[1] + v1._v[2] * v2._v[2];
}
```
On the *device*, it is computed using intrinsics. Here, ```__fmul_rz(float a, float b)``` multiplies two floats with round toward zero rounding:
```cpp
__device__ static constexpr float dot(const vec3& v1, const vec3& v2) {
        return
            (
                __fmul_rz(v1._v[0], v2._v[0])
                + __fmul_rz(v1._v[1], v2._v[1])
                + __fmul_rz(v1._v[2], v2._v[2])
            );
}
```
---

Enjoy this little project as you see fit, and feel free to contact me!

Email: slimlimem@gmail.com Linkedin: https://www.linkedin.com/in/slim-limem/
