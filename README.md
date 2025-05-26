Minimal example for reproduce problem.

The problem is the duplicate object files when using *Unity Build* with *XCode* generator.
In this case all sources in `unity_0_cxx.o` can lose *debug symbols*.

Steps for reproduce:
```cmake
add_library(A OBJECT ${src_A})

add_library(B OBJECT ${src_B})
target_link_libraries(B PRIVATE A)

add_executable(C ${src})
target_link_libraries(C PRIVATE B)
```

For compile full example in this repo use
```bash
cmake --preset=common
cmake --build --preset=common
```
and we get warning
```
warning duplicate member name 'unity_0_cxx.o' from '../test_proj/.build/common/build/lib_wrapper.build/Debug/Objects-normal/arm64/unity_0_cxx.o(unity_0_cxx.o)' and '../test_proj/.build/common/build/mylib.build/Debug/Objects-normal/arm64/unity_0_cxx.o(unity_0_cxx.o)'
```
If try set breakpoint in IDE to `mylib/mylib.cpp:5`, debugger ignore it.

If change object to *static/shared* lib or disable *unity build* the problem disappears.