# CommonLibSSE-NG Plugin Template

Template for building SKSE plugins using the NG branch of CommonLibVR.  

## Requirements

- Any terminal of your choice (e.g., PowerShell)
- [Visual Studio Community 2022](https://visualstudio.microsoft.com/)
  - Desktop development with C++
- [CMake](https://cmake.org/)
  - Edit the `PATH` environment variable and add the cmake.exe install path as a new value
  - Instructions for finding and editing the `PATH` environment variable can be found [here](https://www.java.com/en/download/help/path.html)
  - Note: You will see warnings saying "Unable to locate CMake, CMake Executable" if you miss this step.
- [Git](https://git-scm.com/downloads)
  - Edit the `PATH` environment variable and add the Git.exe install path as a new value
  - Note: You will see warnings saying "Unable to locate Git" if you missed this step.
- [Vcpkg](https://github.com/microsoft/vcpkg)
  - Install vcpkg using the directions in vcpkg's [Quick Start Guide](https://github.com/microsoft/vcpkg#quick-start-windows)
  - After install, add a new environment variable named `VCPKG_ROOT` with the value as the path to the folder containing vcpkg
  - Note: Typically I install this in my `C:/` or `C:/Modding/Code` directory.

## User Requirements

- [Address Library for SKSE](https://www.nexusmods.com/skyrimspecialedition/mods/32444)
  - Needed for SSE/AE
- [VR Address Library for SKSEVR](https://www.nexusmods.com/skyrimspecialedition/mods/58101)
  - Needed for VR
- [Latest x64 Microsoft Visual C++ Redistributable](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170)
  - Probably needed based on what imports you use


## Register Visual Studio as a Generator

- Open `x64 Native Tools Command Prompt`
- Run `cmake`
- Close the cmd window

## Clone and Build
Open terminal (e.g., PowerShell, Git Bash) and run the following commands:

```
git clone https://github.com/Patchu1i/CommonLibSSE-NG-Template.git
cd CommonLibSSE-NG-Template
git submodule init
git submodule update --recursive
```
This should set you up with a local installation of CLib in your project directory ("../extern/CommonLibSSE-NG/"). If the Git Submodule cmd fails, you can do it manually by following these instructions. I don't really know why submodules sometimes don't work when cloning/forking a repo.

```
git submodule deinit --all
<delete the "../extern/" folder in the root project directory>
<open "../.gitmodules" and clear all (CTRL+A, Backspace)>
git submodule add -b ng https://github.com/alandtse/CommonLibVR.git extern/CommonLibSSE-NG
git submodule init
git submodule update --recursive
```

You made need to build the project through the "x64 Native Tools Command Prompt for VS2022" first before building it in VSCode.

1. Open "x64 Native Tools Command Prompt for VS2022".
2. Navigate to your project directory
3. Type `.\BuildRelease.bat SE/AE` to build a release version for SE/AE specifically.
3. Type `.\BuildRelease.bat VR` to build a release version for VR specifically.

## CMake Notes, Project Configuration, Etc.

If you would like to build for NG (SE, AE, and VR), you'll need to create your own preset in `CMakePresets.json` since I don't do this typically. This can easily be done by copying the `SE/AE` preset, renaming it, and also toggling the `ENABLE_SKYRIM_VR` variable.

This project uses the `MSVC` compiler with the `Visual Studio 17 2022` generator. It utilizes CMake, and VPKG for package management. Provided is a baseline package setup. You may want to remove/add to `vcpkg.json` at your discretion.

Make sure to setup your Plugin Name and version in `CMakeLists.txt`.

