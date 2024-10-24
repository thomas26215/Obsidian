---
MOOC: "[[Programmation]]"
Langage: C++
Type: Gtest
tags:
---
```cpp
cmake_minimum_required(VERSION 3.14)
project(RépertoireDuCode)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Inclure Google Test
include(FetchContent)
FetchContent_Declare(
	googletest
	URL https://github.com/google/googletest/archive/03597a01ee50ed33e9dfd640b249b4be3799d395.zip
)
FetchContent_MakeAvailable(googletest)

# Activer les tests
enable_testing()

# Ajouter l'exécutable principal
add_executable(ClasseMain ClasseMain.cpp NomDeLaClasseTestée.cpp)

# Ajouter l'exécutable de test
add_executable(NomDeLaClasseDeTest NomDeLaClasseDeTest.cpp NomDeLaClasseTestée.cpp)
target_link_libraries(NomDeLaClasseDeTests gtest_main)

# Découvrir les tests
include(GoogleTest)
gtest_discover_tests(NomDeLaClasseDeTests)
```