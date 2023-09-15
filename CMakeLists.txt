cmake_minimum_required(VERSION 3.16)

project(OpenCV VERSION 4.8.0)

if (ANDROID)
	function(opencv_add_library TARGET_NAME)
		add_library(${TARGET_NAME} STATIC IMPORTED GLOBAL)

		set_target_properties(${TARGET_NAME}
			PROPERTIES
			IMPORTED_LOCATION "${CMAKE_CURRENT_SOURCE_DIR}/lib/android/${CMAKE_ANDROID_ARCH_ABI}/lib${TARGET_NAME}.a"
			INTERFACE_INCLUDE_DIRECTORIES "${CMAKE_CURRENT_SOURCE_DIR}/include"
			)

		foreach(LIBRARY ${ARGN})
			target_link_libraries(${TARGET_NAME} INTERFACE "${CMAKE_CURRENT_SOURCE_DIR}/lib/android/${CMAKE_ANDROID_ARCH_ABI}/lib${LIBRARY}.a")
		endforeach()

	endfunction()

	opencv_add_library(opencv_core	    ittnotify tegra_hal)
	target_link_libraries(opencv_core   INTERFACE z)

	opencv_add_library(opencv_imgcodecs		libjpeg-turbo libopenjp2 libtiff libpng IlmImf libwebp)
	opencv_add_library(opencv_imgproc)
	opencv_add_library(opencv_objdetect)
	opencv_add_library(opencv_ml)
	opencv_add_library(opencv_highgui)
	opencv_add_library(opencv_calib3d)
	opencv_add_library(opencv_dnn)
	opencv_add_library(opencv_features2d)
	opencv_add_library(opencv_flann)
	opencv_add_library(opencv_gapi)
	opencv_add_library(opencv_photo)
	opencv_add_library(opencv_stitching)
	opencv_add_library(opencv_video)
	opencv_add_library(opencv_videoio)

endif()
