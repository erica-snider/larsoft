# variables to be used in cmake templates
macro( create_product_variables productname productversion )
   string(TOUPPER ${productname} PRODUCTNAME_UC )
   string(TOLOWER ${productname} PRODUCTNAME_LC )

   # require ${PRODUCTNAME_UC}_VERSION
   set( ${PRODUCTNAME_UC}_VERSION "${productversion}" )
   if ( NOT ${PRODUCTNAME_UC}_VERSION )
     message(FATAL_ERROR "product version is not defined")
   endif ()
   STRING( REGEX REPLACE "_" "." VDOT "${productversion}"  )
   STRING( REGEX REPLACE "^[v]" "" ${PRODUCTNAME_UC}_DOT_VERSION "${VDOT}" )
   set( ${PRODUCTNAME_UC}_STRING ${PRODUCTNAME_LC}.${${PRODUCTNAME_UC}_DOT_VERSION} )
   #message(STATUS "${PRODUCTNAME_UC} version is ${${PRODUCTNAME_UC}_VERSION}")
endmacro( create_product_variables)

function(create_version_variables VAR_STEM)
  cmake_parse_arguments(CVV "LIST" "NAME" "QUALIFIERS" ${ARGN})
  if (NOT VAR_STEM)
    message(FATAL_ERROR "vacuous VAR_STEM")
  elseif (NOT CVV_UNPARSED_ARGUMENTS)
    message(FATAL_ERROR "No versions specified")
  endif()
  string(TOUPPER ${VAR_STEM} VAR_STEM_UC)
  list(LENGTH CVV_UNPARSED_ARGUMENTS num_versions)
  if (CVV_LIST OR num_versions GREATER 1)
    set(list_suffix _LIST)
  else()
    set(list_suffix)
  endif()
  string(REPLACE ";" " " versions "${CVV_UNPARSED_ARGUMENTS}")
  set(${VAR_STEM_UC}_VERSION${list_suffix} "${versions}" PARENT_SCOPE)
  set(dot_versions)
  foreach(VERSION ${CVV_UNPARSED_ARGUMENTS})
    string(REPLACE "_" "." VDOT "${VERSION}")
    string(REGEX REPLACE "^v" "" VDOT "${VDOT}")
    list(APPEND dot_versions ${VDOT})
  endforeach()
  string(REPLACE ";" " " dot_versions "${dot_versions}")
  set(${VAR_STEM_UC}_DOT_VERSION${list_suffix}
    "${dot_versions}" PARENT_SCOPE)
  if (NOT CVV_NAME)
    set(CVV_NAME "${VAR_STEM}")
  endif()
  set(${VAR_STEM_UC}_NAME "${CVV_NAME}" PARENT_SCOPE)
  if (CVV_QUALIFIERS)
    set(${VAR_STEM_UC}_QUAL "${CVV_QUALIFIERS}" PARENT_SCOPE)
  endif()
endfunction()

# define qualifiers
set( BASEQUAL e20 )
set( version_set s117 )

set(stack_suffix) # Reset when no longer needed
create_product_variables( larsoft v09_71_00 )
create_product_variables( lardist     ${LARSOFT_VERSION}${stack_suffix} )

create_product_variables( larutils v1_29_01 )
create_product_variables( larbatch v01_59_00 )

create_product_variables( larcoreobj v09_07_00 )
create_product_variables( larcorealg v09_10_00 )
create_product_variables( lardataobj v09_14_00 )
create_product_variables( lardataalg v09_13_03 )
create_product_variables( larvecutils v09_02_00 )
create_product_variables( larsoftobj v09_29_00 )
create_product_variables( larcore v09_08_01 )
create_product_variables( lardata v09_13_01 )
create_product_variables( larevt v09_07_03 )
create_product_variables( larg4 v09_14_01 )
create_product_variables( larsim v09_33_00 )
create_product_variables( larfinder v09_00_01 )
create_product_variables( larsimrad v09_06_15 )
create_product_variables( larsimdnn v09_02_15 )
create_product_variables( larreco v09_17_05 )
create_product_variables( larrecodnn v09_17_14 )
create_product_variables( larana v09_12_04 )
create_product_variables( larpandora v09_19_00 )
create_product_variables( larwirecell v09_12_01 )
create_product_variables( larexamples v09_06_09 )
create_product_variables( lareventdisplay v09_08_11 )
##create_product_variables( webevd v09_10_00 )
create_product_variables( larpandoracontent v04_03_03 )

set(art_suffix)  # Reset when no longer needed
create_product_variables( art v3_09_04 )
create_product_variables( artdist       ${ART_VERSION}${art_suffix} )
create_product_variables( canvas_root_io v1_09_05 )
create_product_variables( gallery v1_18_05 )
create_product_variables( dk2nudata v01_10_01a )
create_product_variables( nusimdata v1_26_02 )
create_product_variables( nutools v3_14_03 )
# the SciSoft bundle containing nutools is named nulite
create_product_variables( nulite v3_14_03 )
create_product_variables( ifdhc_config v2_6_18 )
create_product_variables( genie_xsec v3_04_00 )
create_product_variables( genie_phyopt v3_04_00 )
create_product_variables( glpk          v4_65 )
create_product_variables( guideline_sl  v3_1_0 )
create_product_variables( artg4tk v10_06_00 )
create_product_variables( marley v1_2_0g )
create_product_variables( bxdecay0      v1_0_9 )
create_product_variables( pandora       v03_16_00f )
create_product_variables( pygccxml v2_1_0c )
create_product_variables( hdf5          v1_12_0b )
create_product_variables( h5cpp         v1_10_4_6c )
create_product_variables( hep_hpc       v0_14_01 )
create_product_variables( hep_hpc_toolkit ${HEP_HPC_VERSION}_03 )
create_product_variables( spdlog v1_8_2a )
create_product_variables( wirecell v0_23_0 )
create_product_variables( eigen v3_4_0 )
create_product_variables( jsoncpp       v1_7_7e )
create_product_variables( golang v1_17 )
create_product_variables( gojsonnet v0_17_0 )
#create_product_variables( libtorch      v1_6_0b )
create_product_variables( rstartree v2016_07 )
create_product_variables( opencv        v4_2_0b )
create_product_variables( protobuf      v3_12_3a )
create_product_variables( sundials v5_6_1a )
create_product_variables( stan_math v4_0_1 )
create_product_variables( stan v2_26_1 )
#create_product_variables( grpc          v1_35_0 )
#create_product_variables( triton        v2_3_0b )
create_product_variables( systematicstools v01_02_00 )
create_product_variables( nusystematics v01_02_09 )
create_product_variables( larsoft_data v1_02_02 )
create_version_variables(pycurl v7_45_2)
create_product_variables( mrb v6_08_00 )
create_product_variables( hub           v2_14_2 )
create_product_variables( gh v2_14_4 )
create_product_variables( git v2_37_3 )
# needed for larwire
create_product_variables( libwda v2_30_0a )
create_product_variables( art_root_io v1_08_05 )
# temporary
#create_product_variables( cetpkgsupport v1_14_01 )
create_version_variables(ups v6_1_0)

# CMake, cetbuildtools, and cetmodules are special: 
#  define as many versions as necessary.
create_version_variables(cmake LIST v3_17_3 v3_18_2 v3_19_6 v3_20_0 v3_21_4 v3_22_0 v3_22_2 v3_24_1)
create_version_variables(cetbuildtools LIST v8_18_01 v8_18_04 v8_18_05 v8_18_09 v8_19_02 v8_20_00)
create_version_variables(cetmodules LIST v2_29_02 v2_29_05 v2_29_06 v2_29_12 v2_31_01 v3_02_01 v3_05_03 v3_05_04 v3_06_00 v3_06_01 v3_09_01 v3_09_03 v3_11_03 v3_12_00 v3_13_00 v3_13_02 v3_16_00 v3_20_00 v3_20_00)

# these files should be copied to scisoft for each release
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/lar_product_stack-cfg.in
  ${CMAKE_CURRENT_BINARY_DIR}/lar_product_stack-cfg-${LARDIST_DOT_VERSION} @ONLY )
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/larbase-cfg.in
  ${CMAKE_CURRENT_BINARY_DIR}/larbase-cfg-${LARDIST_DOT_VERSION} @ONLY )
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/larwire-cfg.in
  ${CMAKE_CURRENT_BINARY_DIR}/larwire-cfg-${LARWIRECELL_DOT_VERSION} @ONLY )
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/larsoft-cfg.in
  ${CMAKE_CURRENT_BINARY_DIR}/larsoft-cfg-${LARDIST_DOT_VERSION} @ONLY )
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/larsoftobj-cfg.in
  ${CMAKE_CURRENT_BINARY_DIR}/larsoftobj-cfg-${LARSOFTOBJ_DOT_VERSION} @ONLY )
CONFIGURE_FILE ( ${CMAKE_CURRENT_SOURCE_DIR}/larsoftobj.html.in
  ${CMAKE_CURRENT_BINARY_DIR}/larsoftobj-${LARSOFTOBJ_VERSION}.html @ONLY )
CONFIGURE_FILE ( ${CMAKE_CURRENT_SOURCE_DIR}/larsoft.html.in
  ${CMAKE_CURRENT_BINARY_DIR}/larsoft-${LARDIST_VERSION}.html @ONLY )
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/stan-cfg.in
  ${CMAKE_CURRENT_BINARY_DIR}/stan-cfg-${STAN_DOT_VERSION} @ONLY )

# install releaseDB
INSTALL( FILES base_dependency_database
               README
         DESTINATION "releaseDB" )
