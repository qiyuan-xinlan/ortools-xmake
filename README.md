# ortools-xmake
compile ortools on windows for android
# prepare
- [or-tools source code (only v9.10/v9.12)](https://github.com/google/or-tools/releases/tag/v9.10)
- [cmake](https://cmake.org/download/) 
- [xmake](https://xmake.io/)
- [ndk (recommended version r27c)](https://developer.android.com/ndk/downloads)
- [ninja](https://github.com/ninja-build/ninja)
- [protoc.exe (v26.1 compatible with or-tools v9.10)](https://github.com/protocolbuffers/protobuf/releases/tag/v26.1)
  
# compile
1. in the root directory of the OR-Tools source code, add the [`set(CMAKE_CROSSCOMPILING)`](https://github.com/google/or-tools/discussions/3892) to the `CMakeLists.txt`, and run:
```
xmake f -p android -a arm64-v8a --trybuild=cmake --ndk="ndk_path" --tryconfigs="-DBUILD_DEPS=ON -G Ninja"

xmake
```

2. copy `protoc.exe` to `build\bin\` for debug mode, or `build\RELEASE\bin` for release mode.

3. in `ortools/gscip/gscip_constraint_handler.cc` line **431, 459, 488, 511, 534**: change `SCIPerrorMessage(gresult.status().ToString().c_str());` to `SCIPerrorMessage("%s", gresult.status().ToString().c_str());`  

4. run:
```
cd build

ninja
```
