cmake_minimum_required(VERSION 3.12.0...3.21.0)

project(exodus VERSION 8.9.0 LANGUAGES C)

include(GNUInstallDirs)
include(CMakePackageConfigHelpers)

find_package(MPI REQUIRED)
find_package(hdf5 CONFIG REQUIRED)
find_package(netCDF CONFIG REQUIRED)

set(EXODUS_SOURCES
  src/ex__put_homogenous_block_params.c
  src/ex_add_attr.c
  src/ex_close.c
  src/ex_conv.c
  src/ex_copy.c
  src/ex_create.c
  src/ex_create_group.c
  src/ex_create_par.c
  src/ex_cvt_nodes_to_sides.c
  src/ex_err.c
  src/ex_get_all_times.c
  src/ex_get_assemblies.c
  src/ex_get_assembly.c
  src/ex_get_attr.c
  src/ex_get_attr_names.c
  src/ex_get_attr_param.c
  src/ex_get_attribute.c
  src/ex_get_blob.c
  src/ex_get_blobs.c
  src/ex_get_block.c
  src/ex_get_block_param.c
  src/ex_get_block_params.c
  src/ex_get_cmap_params.c
  src/ex_get_concat_sets.c
  src/ex_get_concat_side_set_node_count.c
  src/ex_get_conn.c
  src/ex_get_coord.c
  src/ex_get_coord_names.c
  src/ex_get_coordinate_frames.c
  src/ex_get_eb_info_global.c
  src/ex_get_elem_cmap.c
  src/ex_get_elem_type.c
  src/ex_get_entity_count_per_polyhedra.c
  src/ex_get_glob_var_time_int.c
  src/ex_get_glob_vars_int.c
  src/ex_get_group_id.c
  src/ex_get_group_ids.c
  src/ex_get_id_map.c
  src/ex_get_ids.c
  src/ex_get_info.c
  src/ex_get_init.c
  src/ex_get_init_ext.c
  src/ex_get_init_global.c
  src/ex_get_init_info.c
  src/ex_get_loadbal_param.c
  src/ex_get_map.c
  src/ex_get_map_param.c
  src/ex_get_name.c
  src/ex_get_names.c
  src/ex_get_nodal_var_int.c
  src/ex_get_nodal_var_time_int.c
  src/ex_get_node_cmap.c
  src/ex_get_ns_param_global.c
  src/ex_get_num_map.c
  src/ex_get_object_truth_vector.c
  src/ex_get_one_attr.c
  src/ex_get_partial_attr.c
  src/ex_get_partial_conn.c
  src/ex_get_partial_coord.c
  src/ex_get_partial_coord_component.c
  src/ex_get_partial_id_map.c
  src/ex_get_partial_nodal_var_int.c
  src/ex_get_partial_num_map.c
  src/ex_get_partial_one_attr.c
  src/ex_get_partial_set.c
  src/ex_get_partial_set_dist_fact.c
  src/ex_get_partial_var.c
  src/ex_get_processor_elem_maps.c
  src/ex_get_processor_node_maps.c
  src/ex_get_prop.c
  src/ex_get_prop_array.c
  src/ex_get_prop_names.c
  src/ex_get_qa.c
  src/ex_get_reduction_variable_name.c
  src/ex_get_reduction_variable_names.c
  src/ex_get_reduction_variable_param.c
  src/ex_get_reduction_vars.c
  src/ex_get_set.c
  src/ex_get_set_dist_fact.c
  src/ex_get_set_param.c
  src/ex_get_sets.c
  src/ex_get_side_set_node_count.c
  src/ex_get_side_set_node_list.c
  src/ex_get_side_set_node_list_len.c
  src/ex_get_ss_param_global.c
  src/ex_get_time.c
  src/ex_get_truth_table.c
  src/ex_get_var.c
  src/ex_get_var_time.c
  src/ex_get_variable_name.c
  src/ex_get_variable_names.c
  src/ex_get_variable_param.c
  src/ex_inquire.c
  src/ex_int_get_block_param.c
  src/ex_ne_util.c
  src/ex_open.c
  src/ex_open_par.c
  src/ex_opts.c
  src/ex_put_all_var_param.c
  src/ex_put_all_var_param_ext.c
  src/ex_put_assemblies.c
  src/ex_put_assembly.c
  src/ex_put_attr.c
  src/ex_put_attr_names.c
  src/ex_put_attr_param.c
  src/ex_put_attribute.c
  src/ex_put_blob.c
  src/ex_put_blobs.c
  src/ex_put_block.c
  src/ex_put_block_param.c
  src/ex_put_block_params.c
  src/ex_put_cmap_params.c
  src/ex_put_cmap_params_cc.c
  src/ex_put_concat_all_blocks.c
  src/ex_put_concat_elem_block.c
  src/ex_put_concat_sets.c
  src/ex_put_conn.c
  src/ex_put_coord.c
  src/ex_put_coord_names.c
  src/ex_put_coordinate_frames.c
  src/ex_put_eb_info_global.c
  src/ex_put_elem_cmap.c
  src/ex_put_entity_count_per_polyhedra.c
  src/ex_put_id_map.c
  src/ex_put_info.c
  src/ex_put_init.c
  src/ex_put_init_ext.c
  src/ex_put_init_global.c
  src/ex_put_init_info.c
  src/ex_put_loadbal_param.c
  src/ex_put_loadbal_param_cc.c
  src/ex_put_map.c
  src/ex_put_map_param.c
  src/ex_put_name.c
  src/ex_put_names.c
  src/ex_put_nodal_var.c
  src/ex_put_nodal_var_int.c
  src/ex_put_node_cmap.c
  src/ex_put_ns_param_global.c
  src/ex_put_num_map.c
  src/ex_put_one_attr.c
  src/ex_put_partial_attr.c
  src/ex_put_partial_conn.c
  src/ex_put_partial_coord.c
  src/ex_put_partial_coord_component.c
  src/ex_put_partial_id_map.c
  src/ex_put_partial_nodal_var_int.c
  src/ex_put_partial_num_map.c
  src/ex_put_partial_one_attr.c
  src/ex_put_partial_set.c
  src/ex_put_partial_set_dist_fact.c
  src/ex_put_partial_var.c
  src/ex_put_processor_elem_maps.c
  src/ex_put_processor_node_maps.c
  src/ex_put_prop.c
  src/ex_put_prop_array.c
  src/ex_put_prop_names.c
  src/ex_put_qa.c
  src/ex_put_reduction_variable_name.c
  src/ex_put_reduction_variable_names.c
  src/ex_put_reduction_variable_param.c
  src/ex_put_reduction_vars.c
  src/ex_put_set.c
  src/ex_put_set_dist_fact.c
  src/ex_put_set_param.c
  src/ex_put_sets.c
  src/ex_put_ss_param_global.c
  src/ex_put_time.c
  src/ex_put_truth_table.c
  src/ex_put_var.c
  src/ex_put_variable_name.c
  src/ex_put_variable_names.c
  src/ex_put_variable_param.c
  src/ex_update.c
  src/ex_utils.c
  )

set(EXODUS_HEADERS
  include/exodusII.h
  include/exodusII_par.h
  include/exodus_config.h
  )

add_library(exodus ${EXODUS_SOURCES})
set_target_properties(exodus PROPERTIES
  PUBLIC_HEADER "${EXODUS_HEADERS}")
target_include_directories(exodus
  PUBLIC
  "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>"
  "$<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>"
  )
target_link_libraries(exodus PUBLIC netCDF::netcdf)
target_link_libraries(exodus PUBLIC MPI::MPI_C)

install(
  TARGETS exodus
  EXPORT exodus-targets
  LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
  ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
  RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
  INCLUDES DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
  PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})

configure_package_config_file(
  "${CMAKE_CURRENT_SOURCE_DIR}/config.cmake.in"
  "${CMAKE_CURRENT_BINARY_DIR}/exodus-config.cmake"
  INSTALL_DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/exodus
)
write_basic_package_version_file(
  "${PROJECT_BINARY_DIR}/exodus-config-version.cmake"
  COMPATIBILITY AnyNewerVersion)

install(FILES
  "${PROJECT_BINARY_DIR}/exodus-config.cmake"
  "${PROJECT_BINARY_DIR}/exodus-config-version.cmake"
  DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/exodus)

install(
  EXPORT exodus-targets
  NAMESPACE exodus::
  DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/exodus)
