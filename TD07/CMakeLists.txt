# la version de cmake à utiliser
cmake_minimum_required(VERSION 3.0)

# La version du C++ que l'on souhaite utiliser (dans notre cas C++17)
set(CMAKE_CXX_STANDARD 20)

# Le nom du projet
project(IMAC_project)

# Réglage du compilateur pour les warnings
if (MSVC)
    add_compile_options(/W3)
else()
    add_compile_options(-Wall -Wextra -Wpedantic -pedantic-errors)
endif()

# On souhaite placer l'exécutable dans un sous-dossier "bin" au lieu de le mettre dans le dossier build
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)

# Obtenir la liste des fichiers sources dans le dossier src
file(GLOB_RECURSE SRC_FILES CONFIGURE_DEPENDS "src/*.cpp")

# Optionnel : afficher la liste des fichiers sources
message(STATUS "Found source files:")
foreach(SRC_FILE ${SRC_FILES})
    message(STATUS " - ${SRC_FILE}")
endforeach()


# On indique que l'on souhaite faire un exécutable avec nos fichiers sources
add_executable(main ${SRC_FILES})

# le dossier contenant les fichiers d'en-tête pour notre executable helloImac
target_include_directories(main PUBLIC "src/")
