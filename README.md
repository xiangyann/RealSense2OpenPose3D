# RealSense2OpenPose3D

This project provides a simple way to use an Intel RealSense depth camera with OpenPose to get 3D keypoints. It was first developed for a Master's project at Advanced Telecommunications Research Institute International (ATR) in Japan.

## Installation

This guide will walk you through all required components.

### Install RealSense SDK:
1. https://github.com/IntelRealSense/librealsense/releases/tag/v2.34.0
	a.	Note: The current version at the time of writing this is v2.50.0. However, there is a bug that prevents the depth and image alignment using “software devices” that was introduced in some build after v2.34.0
	b.	See https://github.com/IntelRealSense/librealsense/issues/4523 for more info

### Install OpenPose:
1.	Prerequisites: https://github.com/CMU-Perceptual-Computing-Lab/openpose/blob/master/doc/installation/1_prerequisites.md
	a.	CMake GUI
		i.	https://cmake.org/download/
		ii.	Download and install cmake-#.#.#-win64-x64.msi
	b.	Install Microsoft Visual Studio
		i.	https://docs.microsoft.com/en-us/visualstudio/releases/2019/release-notes
		ii.	Select all C++ options during installation
	c.	Install CUDA and CuDNN
		i.	Note, must wait until installing Visual studio before proceeding to this step!
		ii.	Install CUDA 11.11 for 30 series GPUs
		iii.	https://developer.nvidia.com/cuda-11.1.1-download-archive?target_os=Windows&target_arch=x86_64&target_version=10&target_type=exenetwork
		iv.	CuDNN
		v.	https://developer.nvidia.com/rdp/cudnn-download
		vi.	Merge files with C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.1
	d.	Install python: https://www.python.org/downloads/windows/
		i.	Install open-cv:
		ii.	In an admin powershell run: pip install numpy opencv-python
2.	Clone OpenPose:
	a.	Create a new folder C:/Program Files/OpenPose
	b.	With an administrator powershell run the following commands
		i.	git clone https://github.com/CMU-Perceptual-Computing-Lab/openpose
		ii.	cd openpose/
		iii.	git submodule update --init --recursive --remote
3.	CMake Configuration
	a.	Enter the OpenPose/openpose
	b.	Make a new folder named “build”
	c.	Enter that new folder
	d.	Run CMake: cmake-gui ..
	e.	Make sure that the source code path field is …OpenPose/openpose and that the build directory is …/OpenPose/openpose/build
	f.	Click “Configure”
	g.	Select the version of Visual Studio that is installed and select x64
	h.	Click “Finish”
	i.	Make sure that the GPU mode is set to CUDA, WITH_3D_RENDERER is on, and WITH_FLIR_CAMERA is off
	j.	Click “Configure” one more time
	k.	Click “Generate”
4.	Compilation:
	a.	Click on “Open Project” to open the Visual Studio solution
	b.	Switch the configuration from “Debug” to “Release”
	c.	Press “F7” (Build)
	d.	Copy all the .dll files from …/build/bin to …/build/x64
5.	Test that it works
	a.	Go to …/OpenPose/openpose/
	b.	Run an example like: build/x64/Release/OpenPoseDemo.exe --video examples/media/video.avi
	c.	Using a camera: build/x64/Release/OpenPoseDemo.exe --hand --face --camera 1

