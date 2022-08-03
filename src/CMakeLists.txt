set(src
  cfl.c
  )

# Static Library
add_library(cfl-static STATIC ${src})

# Install Library
if(MSVC)
  # Rename the output for Windows environment to avoid naming issues
  set_target_properties(cfl-static PROPERTIES OUTPUT_NAME libcfl)
else()
  set_target_properties(cfl-static PROPERTIES OUTPUT_NAME cfl)
endif(MSVC)

install(TARGETS cfl-static
  RUNTIME DESTINATION ${CTR_INSTALL_BINDIR}
  LIBRARY DESTINATION ${CTR_INSTALL_LIBDIR}
  ARCHIVE DESTINATION ${CTR_INSTALL_LIBDIR}
  COMPONENT library)
