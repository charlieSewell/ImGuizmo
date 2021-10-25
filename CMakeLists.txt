project(imguizmo)

add_library(imguizmo STATIC)

target_sources(imguizmo PRIVATE
        src/GraphEditor.cpp
        src/ImCurveEdit.cpp
        src/ImGradient.cpp
        src/ImGuizmo.cpp
        src/ImSequencer.cpp
        )

target_compile_options(imguizmo PRIVATE -fPIC)

target_include_directories(imguizmo PUBLIC . include)
target_link_libraries(imguizmo PRIVATE imgui ${APP_SERVICES_LIBRARY} ${COCOA_LIBRARY})