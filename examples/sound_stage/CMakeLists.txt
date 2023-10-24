include(FetchContent)

FetchContent_Declare(ImGui
    GIT_REPOSITORY https://github.com/ocornut/imgui
    GIT_TAG v1.89.9
    GIT_SHALLOW ON)
FetchContent_MakeAvailable(ImGui)
FetchContent_GetProperties(ImGui SOURCE_DIR IMGUI_DIR)

set(IMGUI_SFML_FIND_SFML OFF)
FetchContent_Declare(ImGui-SFML
    GIT_REPOSITORY https://github.com/SFML/imgui-sfml
    GIT_TAG master
    GIT_SHALLOW ON)
FetchContent_MakeAvailable(ImGui-SFML)
set_target_properties(ImGui-SFML PROPERTIES EXPORT_COMPILE_COMMANDS OFF)
get_target_property(IMGUI_SFML_INCLUDE_DIRS ImGui-SFML INTERFACE_INCLUDE_DIRECTORIES)
target_include_directories(ImGui-SFML SYSTEM INTERFACE ${IMGUI_SFML_INCLUDE_DIRS})

# all source files
set(SRC SoundStage.cpp)

# define the sound-stage target
sfml_add_example(sound-stage GUI_APP
                 SOURCES ${SRC}
                 DEPENDS SFML::Audio SFML::Graphics ImGui-SFML::ImGui-SFML
                 RESOURCES_DIR resources)

# external dependency headers
target_include_directories(sound-stage SYSTEM PRIVATE ${PROJECT_SOURCE_DIR}/examples/sound_stage)
