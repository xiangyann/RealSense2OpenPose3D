# RealSense2OpenPose3D

This project provides a simple way to use an Intel RealSense depth camera with OpenPose to get 3D keypoints. It was first developed for a Master's project at Advanced Telecommunications Research Institute International (ATR) in Japan.

## Installation

This guide will walk you through all required components.

### Install RealSense SDK:
1. https://github.com/IntelRealSense/librealsense/releases/tag/v2.34.0
    1.	Note: The current version at the time of writing this is v2.50.0. However, there is a bug that prevents the depth and image alignment using “software devices” that was introduced in some build after v2.34.0
    2.	See https://github.com/IntelRealSense/librealsense/issues/4523 for more info

### Install OpenPose:
1.	Prerequisites: https://github.com/CMU-Perceptual-Computing-Lab/openpose/blob/master/doc/installation/1_prerequisites.md
    1.	CMake GUI
        1.	https://cmake.org/download/
		2.	Download and install cmake-#.#.#-win64-x64.msi
	2.	Install Microsoft Visual Studio
		1.	https://docs.microsoft.com/en-us/visualstudio/releases/2019/release-notes
		2.	Select all C++ options during installation
	3.	Install CUDA and CuDNN
		1.	Note, must wait until installing Visual studio before proceeding to this step!
		2.	Install CUDA 11.11 for 30 series GPUs
		3.	https://developer.nvidia.com/cuda-11.1.1-download-archive?target_os=Windows&target_arch=x86_64&target_version=10&target_type=exenetwork
		4.	CuDNN
		5.	https://developer.nvidia.com/rdp/cudnn-download
		6.	Merge files with C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.1
	4.	Install python: https://www.python.org/downloads/windows/
		1.	Install open-cv:
		2.	In an admin powershell run: pip install numpy opencv-python
2.	Clone OpenPose:
	1.	Create a new folder C:/Program Files/OpenPose
	2.	With an administrator powershell run the following commands
		1.	git clone https://github.com/CMU-Perceptual-Computing-Lab/openpose
		2.	cd openpose/
		3.	git submodule update --init --recursive --remote
3.	CMake Configuration
	1.	Enter the OpenPose/openpose
	2.	Make a new folder named “build”
	3.	Enter that new folder
	4.	Run CMake: cmake-gui ..
	5.	Make sure that the source code path field is …OpenPose/openpose and that the build directory is …/OpenPose/openpose/build
	6.	Click “Configure”
	7.	Select the version of Visual Studio that is installed and select x64
	8.	Click “Finish”
	9.	Make sure that the GPU mode is set to CUDA, WITH_3D_RENDERER is on, and WITH_FLIR_CAMERA is off
	10.	Click “Configure” one more time
	11.	Click “Generate”
4.	Compilation:
	1.	Click on “Open Project” to open the Visual Studio solution
	2.	Switch the configuration from “Debug” to “Release”
	3.	Press “F7” (Build)
	4.	Copy all the .dll files from …/build/bin to …/build/x64
5.	Test that it works
	1.	Go to …/OpenPose/openpose/
	2.	Run an example like: build/x64/Release/OpenPoseDemo.exe --video examples/media/video.avi
	3.	Using a camera: build/x64/Release/OpenPoseDemo.exe --hand --face --camera 1

