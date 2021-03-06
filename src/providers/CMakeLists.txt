# override default path where built files are put to allow running qgis without installing
SET (CMAKE_RUNTIME_OUTPUT_DIRECTORY ${QGIS_OUTPUT_DIRECTORY}/${QGIS_PLUGIN_SUBDIR})
SET (CMAKE_LIBRARY_OUTPUT_DIRECTORY ${QGIS_OUTPUT_DIRECTORY}/${QGIS_PLUGIN_SUBDIR})

# providers with implemented both static and dynamic building
ADD_SUBDIRECTORY(wms)
IF (POSTGRES_FOUND)
  ADD_SUBDIRECTORY(postgres)
ENDIF (POSTGRES_FOUND)

IF (NOT FORCE_STATIC_PROVIDERS)
  ADD_SUBDIRECTORY(arcgisrest)
  ADD_SUBDIRECTORY(delimitedtext)
  ADD_SUBDIRECTORY(geonode)
  ADD_SUBDIRECTORY(mssql)
  ADD_SUBDIRECTORY(ows)
  ADD_SUBDIRECTORY(wcs)
  ADD_SUBDIRECTORY(gpx)
  ADD_SUBDIRECTORY(wfs)
  ADD_SUBDIRECTORY(spatialite)
  ADD_SUBDIRECTORY(virtual)
  ADD_SUBDIRECTORY(db2)
  ADD_SUBDIRECTORY(mdal)

  IF (WITH_ORACLE)
    ADD_SUBDIRECTORY(oracle)
  ENDIF(WITH_ORACLE)

  IF (WITH_GRASS OR WITH_GRASS7)
    ADD_SUBDIRECTORY(grass)
  ENDIF (WITH_GRASS OR WITH_GRASS7)
ENDIF (NOT FORCE_STATIC_PROVIDERS)
