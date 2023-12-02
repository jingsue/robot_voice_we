cmake_minimum_required(VERSION 3.5)
project(robot_voice)

#Threads

set(CMAKE_THREAD_LIBS_INIT "-lpthread")
set(CMAKE_HAVE_THREADS_LIBRARY 1)
set(CMAKE_USE_WIN32_THREADS_INIT 0)
set(CMAKE_USE_PTHREADS_INIT 1)
set(THREADS_PREFER_PTHREAD_FLAG ON)


# Default to C99
if(NOT CMAKE_C_STANDARD)
  set(CMAKE_C_STANDARD 99)
endif()

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -g -Wall -I${DIR_INC}")

# Choose the platform SDK based on the LINUX64 variable

# find dependencies
find_package(ament_cmake REQUIRED)
# uncomment the following section in order to fill in
# further dependencies manually.
# find_package(<dependency> REQUIRED)

set(SRC /home/llt/robot_voice_ws/src)
set(ROBOT_VOICE ${SRC}/robot_voice)
set(ROBOT_VOICE_INCLUDE ${ROBOT_VOICE}/include)

set(VOICE_PKG_LIB ${CMAKE_HOME_DIRECTORY}/lib/libs/x64)
set(LIB_VOICE ${VOICE_PKG_LIB}/libmsc.so)

find_package(rclcpp REQUIRED)
find_package(std_msgs REQUIRED)
find_package(ALSA REQUIRED)


include_directories(
  include
  ${ROBOT_VOICE_INCLUDE}
)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)

  # the following line skips the linter which checks for copyrights
  # uncomment the line when a copyright and license is not present in all source files
  #set(ament_cmake_copyright_FOUND TRUE)
  # the following line skips cpplint (only works in a git repo)
  # uncomment the line when this package is not in a git repo
  #set(ament_cmake_cpplint_FOUND TRUE)
  ament_lint_auto_find_test_dependencies()
endif()

add_executable(voice_node src/demo.cpp src/linuxrec.c src/speech_recognizer.c)
ament_target_dependencies(voice_node
  rclcpp
  std_msgs
)

target_link_libraries(voice_node ${LIB_VOICE} ${ALSA_LIBRARY})
target_compile_features(voice_node PUBLIC cxx_std_17)

install(TARGETS
voice_node
DESTINATION lib/${PROJECT_NAME})



ament_package()
