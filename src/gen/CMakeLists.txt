# Aseprite Code Generator
# Copyright (C) 2014-2017  David Capello

add_executable(gen
  check_strings.cpp
  gen.cpp
  pref_types.cpp
  strings_class.cpp
  theme_class.cpp
  ui_class.cpp)

if(MSVC)
  # Fix problem compiling gen from a Visual Studio solution
  set_target_properties(gen
    PROPERTIES LINK_FLAGS -ENTRY:"mainCRTStartup")
endif()

if(APPLE)
  #when cross compiling aseprite, make gen compiled as a universal binary.
  set_target_properties(gen laf-base cfg-lib tinyxml
    PROPERTIES OSX_ARCHITECTURES "x86_64;arm64")
endif()

target_link_libraries(gen
  laf-base
  cfg-lib
  ${TINYXML_LIBRARY})
