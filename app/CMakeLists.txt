# For more information about using CMake with Android Studio, read the
# documentation: https://d.android.com/studio/projects/add-native-code.html

# Sets the minimum version of CMake required to build the native library.

#추가부분 start (C:/Users/Saeha/AndroidStudioProjects/CmakeOpenCVTest)
set(pathOpenCv C:/OpenCV-android-sdk)
set(pathProject C:/Users/Saeha/AndroidStudioProjects/FilterTest)
#추가부분 end

cmake_minimum_required(VERSION 3.4.1)

#추가부분 start
set(CMAKE_VERBOSE_MAKEFILE on)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ")

include_directories(${pathOpenCv}/sdk/native/jni/include)
#추가부분 end

# Creates and names a library, sets it as either STATIC
# or SHARED, and provides the relative paths to its source code.
# You can define multiple libraries, and CMake builds them for you.
# Gradle automatically packages shared libraries with your APK.

add_library( # Sets the name of the library.
             native-lib

             # Sets the library as a shared library.
             SHARED

             # Provides a relative path to your source file(s).
             src/main/cpp/native-lib.cpp )

#추가부분 start
add_library( lib_opencv SHARED IMPORTED )
set_target_properties(lib_opencv PROPERTIES IMPORTED_LOCATION ${pathProject}/app/src/main/JniLibs/${ANDROID_ABI}/libopencv_java3.so)
#추가부분 end

# Searches for a specified prebuilt library and stores the path as a
# variable. Because CMake includes system libraries in the search path by
# default, you only need to specify the name of the public NDK library
# you want to add. CMake verifies that the library exists before
# completing its build.

find_library( # Sets the name of the path variable.
              log-lib

              # Specifies the name of the NDK library that
              # you want CMake to locate.
              log )

#추가부분 start
find_library( android-lib android)
#추가부분 end

# Specifies libraries CMake should link to your target library. You
# can link multiple libraries, such as libraries you define in this
# build script, prebuilt third-party libraries, or system libraries.

target_link_libraries( # Specifies the target library.
                       native-lib

                       #추가부분 start
                       lib_opencv
                       #추가부분 end

                       # Links the target library to the log library
                       # included in the NDK.
                       ${log-lib} )