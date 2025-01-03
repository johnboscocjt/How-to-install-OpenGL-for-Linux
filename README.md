# How-to-install-OpenGL-for-Linux
1. Install Dependencies
You'll need to install the necessary libraries: GLFW for window handling and input, and GLAD for loading OpenGL extensions.

On Ubuntu/Debian-based distributions:
Open a terminal and run the following commands:
```bash
# Update package list
sudo apt update

# Install essential development tools and libraries
sudo apt install build-essential

# Install GLFW (Window Management library)
sudo apt install libglfw3-dev

# Install OpenGL (GL development libraries)
sudo apt install libglew-dev libglm-dev

# Install GLAD (OpenGL extension loading library)
sudo apt install cmake
```

OpenGL Setup: GLFW Library
Before you start with creating stunning graphics, you need to initialize an OpenGL context and create an application window to draw in. We’ll do this using a popular C library: GLFW(Graphics Library Framework). This library also helps us handle the input from the joystick, keyboard, and mouse.

Running the below commands would install GLFW in your system:
```bash
cd /usr/local/lib/
git clone https://github.com/glfw/glfw.git
cd glfw
cmake .
make
sudo make install
```
2. Set Up the Project Folder
Create a folder for your project and navigate to it:
```bash
mkdir ~/hello_opengl
cd ~/hello_opengl
```
3. Write the Code
Create a new file hello_triangle.cpp and paste your OpenGL code in it:
```bash
nano hello_triangle.cpp
```
Paste the code and save it.

4. Compile the Program
You’ll need to compile your OpenGL code using g++ (or any C++ compiler), specifying the OpenGL and GLFW libraries to link against.
```bash
g++ hello_triangle.cpp -o hello_triangle -lglfw -lGL -ldl -lX11
```

Explanation of the flags:
-o hello_triangle: Specifies the output file name.
-lglfw: Links the GLFW library.
-lGL: Links the OpenGL library.
-ldl: Links the dynamic loading library (required by GLFW).
-lX11: Links to the X11 library for window management (required by GLFW).

5. Run the Program
Once the program is compiled, you can run it by executing:
```bash
./hello_triangle
```
This should open a window and display the rendered triangle.



Project Structure for OpenGL project
Ensure your project is structured like this:
```bash
openglprojects/
├── glad/
│   ├── include/
│   │ |  └── glad/
│   │ |      └── glad.h
|   | |__KHR/
|   |     └── khrplatform.h
|   | 
│   └── src/glad.c      <-- Make sure this file is present
├── hello_triangle.cpp
└── output/

```


### OTHER:
# USEFUL INFORMATION:
Installation:
1. Have the latest drivers for your graphics card, if you have any
2. Download the latest VS Code IDE
3. Download CMake
4. Download source package GLFW
5. Download Glad:
   from => https://glad.dav1d.de/
   Language: C/C++
   Specification: OpenGL
   API: Version 4.6
   Profile: Compatibility
   Extensions: Will load depending on what you select
   
 Options:
  Checkbox
  Generate a loader
Now, Download the zip file , extract it , and paste it where you write your cpp program:

NOTE:
If you want to find path of glad.c in terminal, in your vs code project, write:
  find . -name "glad.c"



Troubleshooting:
Missing dependencies: If you get errors about missing libraries, ensure you’ve installed all the required packages.
No OpenGL context: Make sure your system has the correct graphics drivers installed.

Using CMake (Recommended for Larger Projects):
If you're working on a larger project and want to organize your build process, it's a good idea to use CMake. Here’s how to set it up:

Create a CMakeLists.txt file:

Create a CMakeLists.txt file in the project directory with the following content:
```bash
cmake_minimum_required(VERSION 3.10)
project(HelloTriangle)

set(CMAKE_CXX_STANDARD 11)

find_package(OpenGL REQUIRED)
find_package(GLFW3 REQUIRED)

add_executable(hello_triangle hello_triangle.cpp)

target_link_libraries(hello_triangle OpenGL::GL GLFW)
```

Build the Project Using CMake:
```bash
mkdir build
cd build
cmake ..
make
```

Run the Program:

After building, you can run your project:
```bash
./hello_triangle
```

#  MORE USEFUL INFO:

Fix Include Path
Modify your hello_triangle.cpp to correctly include GLAD:
```bash
#include "glad/include/glad/glad.h"
```
Or adjust the compiler path to explicitly point to the include directory.

Compile with Correct Flags
Compile with the following command:
```bash
g++ -Wall -Wextra -g3 -I./glad/include -o ./output/hello_triangle hello_triangle.cpp -lglfw -ldl
```
-I./glad/include tells the compiler where to find glad.h.
-lglfw links the GLFW library.
-ldl links to the dynamic loader.

If you face this error:
Please install [clang](http://clang.llvm.org/) or check configuration clang.executable
Do the following:
To use clang as your compiler instead of g++, you need to install clang and configure your editor or IDE to use it.

1. Install Clang:
To install clang on Ubuntu, run the following command:
```bash
sudo apt update
sudo apt install clang
```
Check Clang Installation:
Verify that clang is installed correctly by running:
```bash
clang --version
```
This should output the version of clang you have installed.


Configure clang.executable in VS Code:
If you are using Visual Studio Code, you can configure it to use clang as the compiler:

Open VS Code.
Go to File > Preferences > Settings.
Search for clang.executable.
Set the clang.executable to the path of your clang binary (usually /usr/bin/clang on Ubuntu).

Alternatively, you can configure this in your tasks.json file (in the .vscode folder) like so:
```bash
{
    "version": "2.0.0",
    "tasks": [
        {
            "label": "build hello_triangle",
            "type": "shell",
            "command": "/usr/bin/clang++",
            "args": [
                "-Wall",
                "-Wextra",
                "-g3",
                "-I./glad/include",
                "hello_triangle.cpp",
                "-o",
                "./output/hello_triangle",
                "-lglfw",
                "-ldl"
            ],
            "group": {
                "kind": "build",
                "isDefault": true
            }
        }
    ]
}
```
This configuration will ensure clang++ is used to compile your project.


Build and Run with Clang:
After configuring clang, try building your project again using the VS Code build task or the following command in your terminal:
```bash
clang++ -Wall -Wextra -g3 -I./glad/include hello_triangle.cpp -o ./output/hello_triangle -lglfw -ldl
```

Note:
Ensure Correct Include Order: Include glad before including any other OpenGL headers.
Check for Redundant Headers: If you are using any other libraries that may include OpenGL headers (like GLFW), ensure that they are not including OpenGL headers before glad. If they are, you may need to modify their include order or use #define to prevent them from doing so.
```bash
#include <glad/glad.h>  // Include glad first
#include <GLFW/glfw3.h> // Then include GLFW
```

# Other
1. Update Package List
   ```bash
   sudo apt update
   ```
   Why Use This:
   Updates the package list from the repositories. It ensures that your system has the latest information about the available packages and their versions.
   Without running this, you may install outdated versions of packages.

2. Install Essential Development Tools and Libraries
   ```bash
   sudo apt install build-essential
   ```
  Why Use This:
  Installs essential tools for building and compiling software, such as the gcc/g++ compiler, make utility, and other necessary libraries for development.
  build-essential is a meta-package that includes a standard set of development tools for compiling C, C++, and other code on Linux.
  
3. Install GLFW (Window Management Library)
   ```bash
   sudo apt install libglfw3-dev
   ```
 Why Use This:

  GLFW is a library that helps manage windows, OpenGL contexts, and handle user input (keyboard, mouse, etc.) in OpenGL applications.
  The libglfw3-dev package provides the necessary headers and development files for using GLFW in your OpenGL projects.

4. Install OpenGL Development Libraries
   ```bash
   sudo apt install libglew-dev libglm-dev
   ```
    Why Use This:
    libglew-dev installs the OpenGL Extension Wrangler (GLEW) library, which helps load OpenGL extensions and simplifies access to newer OpenGL features that may not be natively  
    available in your OpenGL version.
    libglm-dev installs the GLM (OpenGL Mathematics) library, a header-only math library useful for working with vectors, matrices, and other mathematical operations commonly used in 
    3D graphics.
   
5. Install GLAD (OpenGL Extension Loading Library)
    ```bash
    sudo apt install cmake
    ```
    Why Use This:

    GLAD is an OpenGL loader used to manage OpenGL function pointers and extensions. You typically need cmake to build GLAD from source, as it uses CMake for its build system.
    The cmake package provides the build system required to configure and generate makefiles for compiling GLAD (and other projects that use CMake). After installing CMake, you'll be     able to download and build GLAD from source if it's not available as a pre-built package.
    By installing these packages, you will have all the necessary development tools, libraries, and environment set up to begin working on OpenGL applications with GLFW, GLEW, and        GLAD.
      






