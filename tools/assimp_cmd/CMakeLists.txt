cmake_minimum_required( VERSION 2.6 )

INCLUDE_DIRECTORIES(
  ${Assimp_SOURCE_DIR}/include
  ${Assimp_SOURCE_DIR}/code
)

LINK_DIRECTORIES( ${Assimp_BINARY_DIR} ${Assimp_BINARY_DIR}/lib )



TARGET_LINK_LIBRARIES( assimp_cmd assimp ${ZLIB_LIBRARIES} )
SET_TARGET_PROPERTIES( assimp_cmd PROPERTIES
  OUTPUT_NAME assimp
)

INSTALL( TARGETS assimp_cmd
  DESTINATION "${ASSIMP_BIN_INSTALL_DIR}" COMPONENT assimp-bin
)
