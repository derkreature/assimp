cmake_minimum_required( VERSION 2.6 )

FIND_PACKAGE(DirectX REQUIRED)

INCLUDE_DIRECTORIES (
  ${Assimp_SOURCE_DIR}/include
  ${Assimp_SOURCE_DIR}/code
  ${DirectX_INCLUDE_DIR}
)

# Make sure the linker can find the Assimp library once it is built.
LINK_DIRECTORIES (${Assimp_BINARY_DIR} ${AssetImporter_BINARY_DIR}/lib)



IF ( MSVC )
  ADD_DEFINITIONS( -D_SCL_SECURE_NO_WARNINGS )
  ADD_DEFINITIONS( -D_CRT_SECURE_NO_WARNINGS )
ENDIF ( MSVC )


#
ADD_CUSTOM_COMMAND(TARGET assimp_viewer
  PRE_BUILD
  COMMAND ${CMAKE_COMMAND} -E copy_if_different $<TARGET_FILE:assimp> $<TARGET_FILE_DIR:assimp_viewer>
  MAIN_DEPENDENCY assimp)

# Link the executable to the assimp + dx libs.
TARGET_LINK_LIBRARIES ( assimp_viewer assimp ${DirectX_LIBRARY} ${DirectX_D3DX9_LIBRARY} comctl32.lib winmm.lib )

INSTALL( TARGETS assimp_viewer
  DESTINATION "${ASSIMP_BIN_INSTALL_DIR}" COMPONENT assimp-dev
)
