cmake_minimum_required(VERSION 3.2)

project(helloworld VERSION 0.0.$ENV{TRAVIS_BUILD_NUMBER})

configure_file(version.h.in version.h)

add_executable(helloworld_cli main.cpp)

add_library(helloworld message.cpp)

set_target_properties(helloworld_cli helloworld PROPERTIES
	CXX_STANDART 14
	CXX_STANDART_REQUIRED ON
	COMPILE_OPTION -Wpedantic -Wall -Wextra
)

target_link_libraries(helloworld_cli 
	helloworld
)

install(TARGETS helloworld_cli RUNTIME DESTINATION bin)

set(CPACK_GENERATOR DEB)

set(CPACK_PACKAGE_VERSION_MAJOR "${PROJECT_VERSION_MAJOR}")
set(CPACK_PACKAGE_VERSION_MINOR "${PROJECT_VERSION_MINOR}")
set(CPACK_PACKAGE_VERSION_PATCH "${PROJECT_VERSION_PATCH}")

set(CPACK_PACKAGE_CONTACT verkin@gmail.com)

include(CPack)