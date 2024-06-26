set(SUBSYS_NAME 2d)
set(SUBSYS_DESC "Point cloud 2d")
set(SUBSYS_DEPS common filters)

PCL_SUBSYS_OPTION(build "${SUBSYS_NAME}" "${SUBSYS_DESC}" ON)
PCL_SUBSYS_DEPEND(build NAME ${SUBSYS_NAME} DEPS ${SUBSYS_DEPS})

PCL_ADD_DOC("${SUBSYS_NAME}")

if(NOT build)
  return()
endif()

set(srcs
  src/convolution_2d.cpp
)

set(incs
  "include/pcl/${SUBSYS_NAME}/convolution.h"
  "include/pcl/${SUBSYS_NAME}/kernel.h"
  "include/pcl/${SUBSYS_NAME}/edge.h"
  "include/pcl/${SUBSYS_NAME}/morphology.h"
)

set(impl_incs
  "include/pcl/${SUBSYS_NAME}/impl/convolution.hpp"
  "include/pcl/${SUBSYS_NAME}/impl/kernel.hpp"
  "include/pcl/${SUBSYS_NAME}/impl/edge.hpp"
  "include/pcl/${SUBSYS_NAME}/impl/morphology.hpp"
)

include_directories("${CMAKE_CURRENT_SOURCE_DIR}/include")

set(LIB_NAME "pcl_${SUBSYS_NAME}")
PCL_MAKE_PKGCONFIG(${LIB_NAME} COMPONENT ${SUBSYS_NAME} DESC ${SUBSYS_DESC} PCL_DEPS ${SUBSYS_DEPS} HEADER_ONLY)

#Install include files
PCL_ADD_INCLUDES("${SUBSYS_NAME}" "${SUBSYS_NAME}" ${incs})
PCL_ADD_INCLUDES("${SUBSYS_NAME}" "${SUBSYS_NAME}/impl" ${impl_incs})
