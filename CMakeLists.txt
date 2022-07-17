project(imguizmo)

SET(SOURCES
        include/GraphEditor.h
        include/ImCurveEdit.h
        include/ImGradient.h
        include/ImGuizmo.h
        include/ImSequencer.h
        include/ImZoomSlider.h
        src/GraphEditor.cpp
        src/ImCurveEdit.cpp
        src/ImGradient.cpp
        src/ImGuizmo.cpp
        src/ImSequencer.cpp
)

add_library(imguizmo STATIC ${SOURCES})

set_target_properties(imguizmo PROPERTIES
        CXX_STANDARD 17
        CXX_STANDARD_REQUIRED ON
        CXX_EXTENSIONS OFF
        VS_DEBUGGER_WORKING_DIRECTORY ${CMAKE_SOURCE_DIR}
)

target_compile_options(imguizmo PRIVATE
        # Clang
        $<$<OR:$<CXX_COMPILER_ID:Clang>,$<CXX_COMPILER_ID:AppleClang>>:
        -Weverything -fcolor-diagnostics
        # Disable specific warnings.
        -Wno-c++98-compat -Wno-c++98-compat-pedantic -Wno-padded
        -Wno-deprecated-declarations -Wno-exit-time-destructors
        -Wno-switch-enum -Wno-weak-vtables -Wno-global-constructors -fPIC>
        # GCC
        $<$<CXX_COMPILER_ID:GNU>:-Wall -Wextra -Wpedantic -fdiagnostics-color=always -fPIC>
        # Visual Studio
        $<$<CXX_COMPILER_ID:MSVC>:/W4 /external:anglebrackets /external:W0>
        # Enable the clang sanitizer.
        $<$<AND:$<CONFIG:Debug>,$<CXX_COMPILER_ID:Clang>,$<PLATFORM_ID:${SANITIZER_OS}>>:${SANITIZER_FLAGS}>
        )

target_link_libraries(imguizmo PRIVATE imgui ${APP_SERVICES_LIBRARY} ${COCOA_LIBRARY})

target_include_directories(imguizmo PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
  $<INSTALL_INTERFACE:>  # <prefix>/include/mylib
)
