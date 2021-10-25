project(imguizmo)

add_library(imguizmo STATIC)

target_sources(imguizmo PRIVATE
        GraphEditor.cpp
        ImCurveEdit.cpp
        ImGradient.cpp
        ImGuizmo.cpp
        ImSequencer.cpp
        )

target_compile_options(imguizmo PRIVATE -fPIC)

target_include_directories(imguizmo PUBLIC . imguizmo)
target_link_libraries(imguizmo PRIVATE imgui ${APP_SERVICES_LIBRARY} ${COCOA_LIBRARY})