
########################################################
# Files

SET (wmts_SRCS
  qgswmts.cpp
  qgswmtsutils.cpp
  qgswmtsgetcapabilities.cpp
  qgswmtsgettile.cpp
  qgswmtsgetfeatureinfo.cpp
  qgswmtsparameters.cpp
)

SET (wmts_MOC_HDRS
  qgswmtsparameters.h
)

########################################################
# Build

QT5_WRAP_CPP(wmts_MOC_SRCS ${wmts_MOC_HDRS})

ADD_LIBRARY (wmts MODULE ${wmts_SRCS} ${wmts_MOC_SRCS} ${wmts_MOC_HDRS})


INCLUDE_DIRECTORIES(SYSTEM
  ${GDAL_INCLUDE_DIR}
  ${POSTGRES_INCLUDE_DIR}
)

INCLUDE_DIRECTORIES(
  ${CMAKE_BINARY_DIR}/src/core
  ${CMAKE_BINARY_DIR}/src/python
  ${CMAKE_BINARY_DIR}/src/analysis
  ${CMAKE_BINARY_DIR}/src/server
  ${CMAKE_CURRENT_BINARY_DIR}
  ../wms
  ../../../core
  ../../../core/dxf
  ../../../core/expression
  ../../../core/geometry
  ../../../core/metadata
  ../../../core/raster
  ../../../core/symbology
  ../../../core/layertree
  ../..
  ..
  .
)


TARGET_LINK_LIBRARIES(wmts
  qgis_core
  qgis_server
)


########################################################
# Install

INSTALL(TARGETS wmts
    RUNTIME DESTINATION ${QGIS_SERVER_MODULE_DIR}
    LIBRARY DESTINATION ${QGIS_SERVER_MODULE_DIR}
)

