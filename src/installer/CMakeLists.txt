#
#   Copyright 2019 Amazon.com, Inc. or its affiliates. All Rights Reserved.
#
#   Licensed under the Apache License, Version 2.0 (the "License").
#   You may not use this file except in compliance with the License.
#   A copy of the License is located at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
#   or in the "license" file accompanying this file. This file is distributed
#   on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either
#   express or implied. See the License for the specific language governing
#   permissions and limitations under the License.
#


# This is a unique id for the installer - required for Windows
# Generated at https://www.guidgen.com/
set(CPACK_WIX_UPGRADE_GUID "2D325BD7-1176-40E8-8AB8-C52DD2F7B792")

# Loop runtime
include(InstallRequiredSystemLibraries)
install(TARGETS elasticodbc DESTINATION bin)

### install(FILES ${CMAKE_INSTALL_SYSTEM_RUNTIME_LIBS} DESTINATION bin COMPONENT Libraries)
#foreach(runtime ${CMAKE_INSTALL_SYSTEM_RUNTIME_LIBS})
#    MESSAGE( STATUS "Including runtime " ${runtime} )
#    #set(CPACK_WIX_UPGRADE_GUID "F9AAAAE2-D6AF-4EA4-BF46-B3E265400CC5")
#    install(FILES ${runtime} DESTINATION bin COMPONENT Libraries)
#endforeach()

set(CPACK_PACKAGE_NAME "opendistro-for-elasticsearch-sql-odbc")
set(CPACK_PACKAGE_DESCRIPTION_SUMMARY "Elasticsearch SQL ODBC Driver")
set(CPACK_PACKAGE_DESCRIPTION_FILE "${PROJECT_ROOT}/README.md")
set(CPACK_PACKAGE_VENDOR "Amazon.com")
set(CPACK_PACKAGE_CONTACT "someemail@foo.blah")
set(CPACK_PACKAGE_INSTALL_DIRECTORY "${CPACK_PACKAGE_NAME}")
set(CPACK_SYSTEM_NAME "${CMAKE_SYSTEM_NAME}")

# Wix doesn't allow extensionless licenses, need to make a copy with an extension, .txt is appropriate
configure_file("${PROJECT_ROOT}/LICENSE" "${PROJECT_ROOT}/LICENSE.txt" COPYONLY)
set(CPACK_RESOURCE_FILE_LICENSE "${PROJECT_ROOT}/LICENSE.txt")

# Set install package version to our package version
set(CPACK_PACKAGE_VERSION "${PACKAGE_VERSION}")

# Set generator to WIX
set(CPACK_GENERATOR "WIX")

include(CPack)