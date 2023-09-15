# OpenCV v4.8.0 prebuilt libraries for Android
---
- Built OpenCV 4.8.0 static libraries in release modes
- Sources retrieved from [the official GitHub OpenCV repository](https://github.com/opencv/opencv/tree/4.8.0)
- **Android ABI: arm64-v8a, armeabi-v7a**
---
## How to Use

The simplest way to add OpenCV to your CMake project is to use FetchContent module functionality.
Just add the following lines to your CMakeLists.txt file. 

```cmake

include(FetchContent)

FetchContent_Declare(
	OpenCV
	GIT_REPOSITORY			https://github.com/S-Pasternak/opencv-android.git
	GIT_TAG        			4.8.0
	GIT_SHALLOW 			ON
	UPDATE_DISCONNECTED		ON
)

FetchContent_MakeAvailable(OpenCV)

```

Then any of OpenCV modules can be included in project with command target_link_libraries

```cmake

add_library(MyLibrary SHARED MyLibrary.cpp)

target_link_libraries(MyLibrary opencv_core, opencv_imgproc)

```
---
## OpenCV Modules

- opencv_core - ["Core functionality"](https://docs.opencv.org/4.8.0/d0/de1/group__core.html)
- opencv_imgproc - ["Image Processing"](https://docs.opencv.org/4.8.0/d7/dbd/group__imgproc.html)
- opencv_imgcodecs - ["Image file reading and writing"](https://docs.opencv.org/4.8.0/d4/da8/group__imgcodecs.html)
- opencv_videoio - ["Video I/O"](https://docs.opencv.org/4.8.0/dd/de7/group__videoio.html)
- opencv_highgui - ["High-level GUI"](https://docs.opencv.org/4.8.0/d7/dfc/group__highgui.html)
- opencv_video - ["Video Analysis"](https://docs.opencv.org/4.8.0/d7/de9/group__video.html)
- opencv_calib3d - ["Camera Calibration and 3D Reconstruction"](https://docs.opencv.org/4.8.0/d9/d0c/group__calib3d.html)
- opencv_features2d - ["2D Features Framework"](https://docs.opencv.org/4.8.0/da/d9b/group__features2d.html)
- opencv_objdetect - ["Object Detection"](https://docs.opencv.org/4.8.0/d5/d54/group__objdetect.html)
- opencv_dnn - ["Deep Neural Network module"](https://docs.opencv.org/4.8.0/d6/d0f/group__dnn.html)
- opencv_ml - ["Machine Learning"](https://docs.opencv.org/4.8.0/dd/ded/group__ml.html)
- opencv_flann - ["Clustering and Search in Multi-Dimensional Spaces"](https://docs.opencv.org/4.8.0/dc/de5/group__flann.html)
- opencv_photo - ["Computational Photography"](https://docs.opencv.org/4.8.0/d1/d0d/group__photo.html)
- opencv_stitching - ["Images stitching"](https://docs.opencv.org/4.8.0/d1/d46/group__stitching.html)
- opencv_gapi - ["Graph API"](Graph API)

---
## Build Details

```bash

OPENCV_VERSION="4.8.0"

# 1. Retrieve OpenCV sources from official repository
git clone --branch ${OPENCV_VERSION} --depth 1 https://github.com/opencv/opencv.git

# 2. Set Android ABI (possible values: arm64-v8a, armeabi-v7a, x86, x86_64)
ARCHITECTURE=arm64-v8a

# 3. Create build directory
mkdir ./build-${ARCHITECTURE}
cd ./build-${ARCHITECTURE}

# 4. Configure build 
cmake ../opencv \
	-G"Ninja Multi-Config" \
	-DCMAKE_SYSTEM_NAME=Android \
	-DCMAKE_ANDROID_ARCH_ABI=${ARCHITECTURE} \
	-DBUILD_SHARED_LIBS=OFF \
	-DBUILD_ANDROID_PROJECTS=OFF \
	-DBUILD_ANDROID_EXAMPLES=OFF \
	-DBUILD_JAVA=OFF \
	-DBUILD_KOTLIN_EXTENSIONS=OFF \
	-DBUILD_FAT_JAVA_LIB=OFF

# 5. Build OpenCV library
cmake --build . --parallel --config release
cmake --install . --config release

# Repeat steps 2 through 5 for other Android ABIs

```