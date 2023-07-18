# docker-nav2-humble

## Build Container

1. git clone https://github.com/vishwaslip/docker-nav2-humble.git
2. Open `docker-nav2-humble` in vscode
3. `ctrl+shift+p` to open command browser, tpye and select: `Dev Containers: Rebuild and Reopen in Container`

*Takes a while to build.
*Password: password

## Reproducing Nav 2 Build Error

1. `sudo mkdir -p /opt/ros/nav2/src && cd /opt/ros/nav2/src`
2. `sudo git clone https://github.com/ros-planning/navigation2.git --branch humble`
3. `source /opt/ros/${ROS2_DISTRO}/install/setup.bash && cd /opt/ros/nav2`
4. `vcs import src < /path/to/nav2_humble_dependencies.repos` *Current tools/underlay.repos file in humble does not work.
5. `rosdep update && rosdep install -y --ignore-src --from-paths src`
6. `colcon build --merge-install`

### Expected behavior

Should build Nav 2

### Actual Behavior

nav2_smac_planner errors:

```
CMake Error at CMakeLists.txt:75 (add_library):
  Target "nav2_smac_planner" links to target "Boost::serialization" but the
  target was not found.  Perhaps a find_package() call is missing for an
  IMPORTED target, or an ALIAS target is missing?


CMake Error at CMakeLists.txt:75 (add_library):
  Target "nav2_smac_planner" links to target "Boost::filesystem" but the
  target was not found.  Perhaps a find_package() call is missing for an
  IMPORTED target, or an ALIAS target is missing?


CMake Error at CMakeLists.txt:75 (add_library):
  Target "nav2_smac_planner" links to target "Boost::system" but the target
  was not found.  Perhaps a find_package() call is missing for an IMPORTED
  target, or an ALIAS target is missing?

  ...

  CMake Error at /opt/ros/humble/install/share/ament_cmake_gtest/cmake/ament_add_gtest_executable.cmake:50 (add_executable):
  Target "test_lattice_node" links to target "Boost::filesystem" but the
  target was not found.  Perhaps a find_package() call is missing for an
  IMPORTED target, or an ALIAS target is missing?
Call Stack (most recent call first):
  /opt/ros/humble/install/share/ament_cmake_gtest/cmake/ament_add_gtest_executable.cmake:37 (_ament_add_gtest_executable)
  /opt/ros/humble/install/share/ament_cmake_gtest/cmake/ament_add_gtest.cmake:68 (ament_add_gtest_executable)
  test/CMakeLists.txt:114 (ament_add_gtest)


CMake Error at /opt/ros/humble/install/share/ament_cmake_gtest/cmake/ament_add_gtest_executable.cmake:50 (add_executable):
  Target "test_lattice_node" links to target "Boost::system" but the target
  was not found.  Perhaps a find_package() call is missing for an IMPORTED
  target, or an ALIAS target is missing?
Call Stack (most recent call first):
  /opt/ros/humble/install/share/ament_cmake_gtest/cmake/ament_add_gtest_executable.cmake:37 (_ament_add_gtest_executable)
  /opt/ros/humble/install/share/ament_cmake_gtest/cmake/ament_add_gtest.cmake:68 (ament_add_gtest_executable)
  test/CMakeLists.txt:114 (ament_add_gtest)


CMake Generate step failed.  Build files cannot be regenerated correctly.
---
Failed   <<< nav2_smac_planner [1min 40s, exited with code 1]
```

### Additional information

This setup should install libboost-all-dev version 1.74. But errors. 


