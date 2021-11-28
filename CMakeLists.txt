cmake_minimum_required(VERSION 3.15)

enable_language(CXX)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

project(NewProject VERSION 1.0.0)

add_subdirectory(External/JUCE)

juce_add_gui_app(NewProject
    PRODUCT_NAME "NewProject")

juce_generate_juce_header(NewProject)

target_sources(NewProject
    PRIVATE
        Source/Main.cpp
        Source/MainComponent.h
        Source/MainComponent.cpp)

target_compile_definitions(NewProject
    PRIVATE
        JUCE_APPLICATION_NAME_STRING="$<TARGET_PROPERTY:NewProject,JUCE_PRODUCT_NAME>"
        JUCE_APPLICATION_VERSION_STRING="$<TARGET_PROPERTY:NewProject,JUCE_VERSION>")

target_link_libraries(NewProject
    PRIVATE
        juce::juce_audio_utils
    PUBLIC
        juce::juce_recommended_config_flags
        juce::juce_recommended_lto_flags
        juce::juce_recommended_warning_flags)