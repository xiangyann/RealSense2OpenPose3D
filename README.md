# RealSense2OpenPose3D

This project provides a simple way to use an [**Intel RealSense depth camera**](https://www.intelrealsense.com/depth-camera-d435/) with [**OpenPose**](https://github.com/CMU-Perceptual-Computing-Lab/openpose) to get 3D keypoints. It was first developed for a Master's project while doing an internship at [Advanced Telecommunications Research Institute International (ATR)](https://www.atr.jp/index_e.html).

## Use
1. After installing all required components and either compiling or downloading OpenPose2RealSense3D, edit the default paths in the `launch.py` file to match your layout.
	1. You may also specify the paths later as command line arguments if you so desire
2. Run the program by entering `python .\launch.py` into a console where the launch file is located.
3. Arguments (do not enter spaces after the '='):
	1. `frames=` number >= -1. Is the number of frames beyond 10 that will not be deleted during run time (-1 is save all)
	2. `view=` True or false. Whether to start the point viewer or not
	3. `quit=` An alphanumeric character. This determines which keyboard key will terminate the program
	4. `d=` float number >= 0. The depth limit beyond which values are ignored
	5. `lr=` float number >= 0`,`float number >= 0. The right and left limits of the point viwer in meters
	6. `ud=` float number >= 0`,`float number >= 0. The up and down limits of the point viwer in meters
	7. Other input will yield the help menu
	8. Example: `python .\launch.py frames=-1 view=true quit=q d=2.5 lr=1.5,1.5 ud=1,1`
4. The output files will be marked as `############_keypointsD.json` in the output folder
5. See [**OpenPose's documentation**](https://github.com/CMU-Perceptual-Computing-Lab/openpose/blob/master/doc/02_output.md) for the format of the output JSON files

## Installation

This guide will walk you through all required components.

### Install RealSense SDK:
1. [Download RealSense SDK v2.34](https://github.com/IntelRealSense/librealsense/releases/tag/v2.34.0)
    1.	Note: The current version at the time of writing this is v2.50.0. However, there is a bug that prevents the depth and image alignment using “software devices” that was introduced in some build after v2.34.0
    2.	See [this issue](https://github.com/IntelRealSense/librealsense/issues/4523) for more info

### Install OpenPose:
1.	Prerequisites: [Prerequisite List](https://github.com/CMU-Perceptual-Computing-Lab/openpose/blob/master/doc/installation/1_prerequisites.md)
    1.	CMake GUI
        1.	[Download page](https://cmake.org/download/)
		2.	Download and install `cmake-#.#.#-win64-x64.msi`
	2.	Install Microsoft Visual Studio
		1.	[Download page](https://docs.microsoft.com/en-us/visualstudio/releases/2019/release-notes)
		2.	Select all C++ options during installation
	3.	Install CUDA and CuDNN
		1.	*Note:* You must wait until after installing Visual Studio before proceeding to this step!
		2.	Install CUDA 11.11 for 30 series GPUs
		3.	[CUDA download page](https://developer.nvidia.com/cuda-11.1.1-download-archive?target_os=Windows&target_arch=x86_64&target_version=10&target_type=exenetwork)
		4.	CuDNN
		5.	[CuDNN download page](https://developer.nvidia.com/rdp/cudnn-download)
		6.	Merge files with `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.1`
	4.	Install python: [Download Page](https://www.python.org/downloads/windows/)
		1.	Install open-cv:
		2.	In an admin powershell run: `pip install numpy opencv-python`
2.	Clone OpenPose:
	1.	Create a new folder `C:/Program Files/OpenPose`
	2.	With an administrator powershell run the following commands
		<pre><code>git clone https://github.com/CMU-Perceptual-Computing-Lab/openpose
		cd openpose/
		git submodule update --init --recursive --remote</code></pre>
3.	CMake Configuration
	1.	Enter the `OpenPose/openpose` directory
	2.	Make a new folder named “build”
	3.	Enter that new folder
	4.	Run CMake: `cmake-gui ..`
	5.	Make sure that the source code path field is `…OpenPose/openpose` and that the build directory is `…/OpenPose/openpose/build`
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
	4.	Copy all the .dll files from `…/build/bin` to `…/build/x64`
5.	Test that it works
	1.	Go to …/OpenPose/openpose/
	2.	Run an example like: `build/x64/Release/OpenPoseDemo.exe --video examples/media/video.avi`
	3.	Using a camera: `build/x64/Release/OpenPoseDemo.exe --hand --face --camera 1`

