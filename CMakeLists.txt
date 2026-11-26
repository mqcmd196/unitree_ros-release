cmake_minimum_required(VERSION 3.12)
project(g1_description)

find_package(ament_cmake REQUIRED)

# Generate ROS resource URLs without modifying upstream URDFs.
file(GLOB urdf_files CONFIGURE_DEPENDS "${CMAKE_CURRENT_SOURCE_DIR}/*.urdf")
set_property(DIRECTORY APPEND PROPERTY CMAKE_CONFIGURE_DEPENDS ${urdf_files})
foreach(urdf_file IN LISTS urdf_files)
  get_filename_component(urdf_name "${urdf_file}" NAME)
  file(READ "${urdf_file}" urdf_content)
  string(REPLACE "filename=\"meshes/" "filename=\"package://${PROJECT_NAME}/meshes/"
    urdf_content "${urdf_content}")
  file(WRITE "${CMAKE_CURRENT_BINARY_DIR}/${urdf_name}" "${urdf_content}")
  install(FILES "${CMAKE_CURRENT_BINARY_DIR}/${urdf_name}"
    DESTINATION share/${PROJECT_NAME})
endforeach()

file(GLOB mjcf_files CONFIGURE_DEPENDS "${CMAKE_CURRENT_SOURCE_DIR}/g1*.xml")
install(FILES ${mjcf_files} DESTINATION share/${PROJECT_NAME})
install(DIRECTORY meshes inspire_hand images launch
  DESTINATION share/${PROJECT_NAME})

ament_package()
