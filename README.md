A C++ project template for Vulkan (GLFW + GLM + OpenGL) projects that builds on Linux, Mac, and Windows using CMake.

GLFW, and GLM are automatically downloaded from GitHub and compiled (in case of GLFW). There's no need to install any other libraries.


After cloning repository, run:

```
cmake -B build -S .
```

then you run

```
cmake --build build
```

If you want to cleanup everything

```
./bin/cleanup.bat
```

Tested on Windows so if any errors please write or contribute.