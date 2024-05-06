[![Build Status](https://app.travis-ci.com/Rigrey/lab04.svg?token=sSjKqXpxzeqqaxAwq5f2&branch=main)](https://app.travis-ci.com/Rigrey/lab04)

# tp-lab06
Study of batching tools using CPack as an example.

## Tutorial

```sh
❯ export GITHUB_USERNAME=TheIIIrd
❯ export GITHUB_EMAIL=metexas109@etopys.com
❯ alias edit=nvim
❯ alias gsed=sed
```

```sh
❯ cd ${GITHUB_USERNAME}/workspace
❯ pushd .
❯ source scripts/activate
```

```sh
❯ git clone git@github.com:${GITHUB_USERNAME}/tp-lab05.git projects/lab06 
Cloning into 'projects/lab06'...
remote: Enumerating objects: 47, done.
remote: Counting objects: 100% (47/47), done.
remote: Compressing objects: 100% (28/28), done.
remote: Total 47 (delta 16), reused 42 (delta 14), pack-reused 0
Receiving objects: 100% (47/47), 30.41 KiB | 97.00 KiB/s, done.
Resolving deltas: 100% (16/16), done.

❯ cd projects/lab06
❯ git remote remove origin
❯ git remote add origin git@github.com:${GITHUB_USERNAME}/tp-lab06.git
```

```sh
❯ sed -i '/project(print)/a\ 
set(PRINT_VERSION_STRING "v\${PRINT_VERSION}")
' CMakeLists.txt

❯ sed -i '/project(print)/a\
set(PRINT_VERSION\
  \${PRINT_VERSION_MAJOR}.\${PRINT_VERSION_MINOR}.\${PRINT_VERSION_PATCH}.\${PRINT_VERSION_TWEAK})
' CMakeLists.txt

❯ sed -i '/project(print)/a\
set(PRINT_VERSION_TWEAK 0)
' CMakeLists.txt

❯ sed -i '/project(print)/a\
set(PRINT_VERSION_PATCH 0)
' CMakeLists.txt

❯ sed -i '/project(print)/a\
set(PRINT_VERSION_MINOR 1)
' CMakeLists.txt

❯ sed -i '/project(print)/a\
set(PRINT_VERSION_MAJOR 0)
' CMakeLists.txt
```

```sh
❯ git diff 
diff --git a/CMakeLists.txt b/CMakeLists.txt
index 96a361e..db651c5 100644
--- a/CMakeLists.txt
+++ b/CMakeLists.txt
@@ -6,6 +6,13 @@ set(CMAKE_CXX_STANDARD_REQUIRED ON)
 option(BUILD_EXAMPLES "Build examples" OFF)
 
 project(print)
+set(PRINT_VERSION_MAJOR 0)
+set(PRINT_VERSION_MINOR 1)
+set(PRINT_VERSION_PATCH 0)
+set(PRINT_VERSION_TWEAK 0)
+set(PRINT_VERSION
+  ${PRINT_VERSION_MAJOR}.${PRINT_VERSION_MINOR}.${PRINT_VERSION_PATCH}.${PRINT_VERSION_TWEAK})
+set(PRINT_VERSION_STRING "v${PRINT_VERSION}")
 
 add_library(print STATIC ${CMAKE_CURRENT_SOURCE_DIR}/sources/print.cpp)
```

```sh
❯ nvim DESCRIPTION 
❯ touch ChangeLog.md
❯ export DATE="`LANG=en_US date +'%a %b %d %Y'`" 
```

```sh
❯ cat > ChangeLog.md <<EOF
* ${DATE} ${GITHUB_USERNAME} <${GITHUB_EMAIL}> 0.1.0.0
- Initial RPM release
EOF

❯ cat > CPackConfig.cmake <<EOF
include(InstallRequiredSystemLibraries)
EOF

❯ cat >> CPackConfig.cmake <<EOF
set(CPACK_PACKAGE_CONTACT ${GITHUB_EMAIL})
set(CPACK_PACKAGE_VERSION_MAJOR \${PRINT_VERSION_MAJOR})
set(CPACK_PACKAGE_VERSION_MINOR \${PRINT_VERSION_MINOR})
set(CPACK_PACKAGE_VERSION_PATCH \${PRINT_VERSION_PATCH})
set(CPACK_PACKAGE_VERSION_TWEAK \${PRINT_VERSION_TWEAK})
set(CPACK_PACKAGE_VERSION \${PRINT_VERSION})
set(CPACK_PACKAGE_DESCRIPTION_FILE \${CMAKE_CURRENT_SOURCE_DIR}/DESCRIPTION)
set(CPACK_PACKAGE_DESCRIPTION_SUMMARY "static C++ library for printing")
EOF

❯ cat >> CPackConfig.cmake <<EOF

set(CPACK_RESOURCE_FILE_LICENSE \${CMAKE_CURRENT_SOURCE_DIR}/LICENSE)
set(CPACK_RESOURCE_FILE_README \${CMAKE_CURRENT_SOURCE_DIR}/README.md)
EOF

❯ cat >> CPackConfig.cmake <<EOF

set(CPACK_RPM_PACKAGE_NAME "print-devel")
set(CPACK_RPM_PACKAGE_LICENSE "MIT")
set(CPACK_RPM_PACKAGE_GROUP "print")
set(CPACK_RPM_CHANGELOG_FILE \${CMAKE_CURRENT_SOURCE_DIR}/ChangeLog.md)
set(CPACK_RPM_PACKAGE_RELEASE 1)
EOF

❯ cat >> CPackConfig.cmake <<EOF

set(CPACK_DEBIAN_PACKAGE_NAME "libprint-dev")
set(CPACK_DEBIAN_PACKAGE_PREDEPENDS "cmake >= 3.0")
set(CPACK_DEBIAN_PACKAGE_RELEASE 1)
EOF

❯ cat >> CPackConfig.cmake <<EOF

include(CPack)
EOF

❯ cat >> CMakeLists.txt <<EOF

include(CPackConfig.cmake)
EOF
```

```sh
❯ sed -i 's/lab05/lab06/g' README.md
```

```sh
❯ git add .
❯ git commit -m "added cpack config"
[main d7100f1] added cpack config
 5 files changed, 61 insertions(+), 24 deletions(-)
 create mode 100644 CPackConfig.cmake
 create mode 100644 ChangeLog.md
 create mode 100644 DESCRIPTION
```

```sh
❯ git tag v0.1.0.0
❯ git push origin main --tags
Enumerating objects: 54, done.
Counting objects: 100% (54/54), done.
Delta compression using up to 4 threads
Compressing objects: 100% (33/33), done.
Writing objects: 100% (54/54), 31.57 KiB | 31.57 MiB/s, done.
Total 54 (delta 19), reused 44 (delta 16), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (19/19), done.
To github.com:TheIIIrd/tp-lab06.git
 * [new branch]      main -> main
 * [new tag]         v0.1.0.0 -> v0.1.0.0
```

```sh
❯ cmake -H. -B_build
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- The C compiler identification is GNU 13.2.1
-- The CXX compiler identification is GNU 13.2.1
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /sbin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /sbin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done (0.4s)
-- Generating done (0.0s)
-- Build files have been written to: lab06/_build
```

```sh
❯ cmake --build _build                                 
[ 50%] Building CXX object CMakeFiles/print.dir/sources/print.cpp.o
[100%] Linking CXX static library libprint.a
[100%] Built target print
```

```sh
❯ cd _build 
❯ cpack -G "TGZ" 
CPack: Create package using TGZ
CPack: Install projects
CPack: - Run preinstall target for: print
CPack: - Install project: print []
CPack: Create package
CPack: - package: lab06/_build/print-0.1.0.0-Linux.tar.gz generated.

❯ cd ..
```

```
❯ cmake -H. -B_build -DCPACK_GENERATOR="TGZ" 
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- Configuring done (0.0s)
-- Generating done (0.0s)
-- Build files have been written to: lab06/_build
```

```sh                                                                                          
❯ cmake --build _build --target package 
[100%] Built target print
Run CPack packaging tool...
CPack: Create package using TGZ
CPack: Install projects
CPack: - Run preinstall target for: print
CPack: - Install project: print []
CPack: Create package
CPack: - package: lab06/_build/print-0.1.0.0-Linux.tar.gz generated.

❯ mkdir artifacts                                                                                            
❯ mv _build/*.tar.gz artifacts
```

```sh                                                                                         
❯ sudo pacman -Syy tree
:: Synchronizing package databases...
 core                                                    121.7 KiB  99.9 MiB/s 00:00 [#################################################] 100%
 extra                                                     7.8 MiB  99.9 MiB/s 00:03 [#################################################] 100%
 multilib                                                140.5 KiB  99.9 MiB/s 00:00 [#################################################] 100%
resolving dependencies...
looking for conflicting packages...

Packages (1) tree-2.1.1-1

Total Download Size:   0.04 MiB
Total Installed Size:  0.09 MiB

:: Proceed with installation? [Y/n] 
:: Retrieving packages...
 tree-2.1.1-1-x86_64                                      39.4 KiB  99.9 MiB/s 00:00 [#################################################] 100%
(1/1) checking keys in keyring                                                       [#################################################] 100%
(1/1) checking package integrity                                                     [#################################################] 100%
(1/1) loading package files                                                          [#################################################] 100%
(1/1) checking for file conflicts                                                    [#################################################] 100%
(1/1) checking available disk space                                                  [#################################################] 100%
:: Processing package changes...
(1/1) installing tree                                                                [#################################################] 100%
:: Running post-transaction hooks...
(1/1) Arming ConditionNeedsUpdate...

❯ tree artifacts  
artifacts
└── print-0.1.0.0-Linux.tar.gz
```
1 directory, 1 file
