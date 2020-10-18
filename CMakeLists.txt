cmake_minimum_required(VERSION 3.18.X)
project(HelloTriangle_Project LANGUAGES CXX)
add_executable(HelloTriangle main.cxx)
target_compile_features(HelloTriangle PRIVATE cxx_std_17)

# -----------------------------------------------------
# (*) brew install glfw3 --HEAD
# (*) brew install glm
# (*) LunarG SDK Vulkan

#Finding and linking GLFW3 (windowing, context & input)
find_package(GLFW3 3.3 REQUIRED)
if (GLFW3_FOUND)
    message("GLFW3 FOUND")
    target_link_libraries(HelloTriangle glfw)
endif (GLFW3_FOUND)

#Finding and linking Vulkan
#https://cmake.org/cmake/help/latest/module/FindVulkan.html
find_package (Vulkan REQUIRED)
if (Vulkan_FOUND)
    message("Vulkan FOUND")
    include_directories(${Vulkan_INCLUDE_DIRS})
    target_link_libraries (HelloTriangle ${Vulkan_LIBRARIES})
    message("Vulkan_INCLUDE_DIRS : " ${Vulkan_INCLUDE_DIRS})
    message("Vulkan_LIBRARIES : " ${Vulkan_LIBRARIES})
endif (Vulkan_FOUND)

#Finding and linking glm (linear algebra math library)
find_package(GLM REQUIRED)
if (GLM_FOUND)
    message("GLM FOUND")
endif (GLM_FOUND)
