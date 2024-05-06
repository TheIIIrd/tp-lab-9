[![Build Status](https://app.travis-ci.com/Rigrey/lab04.svg?token=sSjKqXpxzeqqaxAwq5f2&branch=main)](https://app.travis-ci.com/Rigrey/lab04)

# tp-lab06

Exploring frameworks for testing using GTest as an example.

## Tutorial

```sh
❯ export GITHUB_USERNAME=TheIIIrd
❯ alias gsed=sed
❯ cd ${GITHUB_USERNAME}/workspace
❯ pushd .
~/TheIIIrd/workspace ~/TheIIIrd/workspace

source scripts/activate
```

```sh
❯ git clone git@github.com:${GITHUB_USERNAME}/tp-lab04.git projects/lab06                   
Cloning into 'projects/lab06'...
remote: Enumerating objects: 40, done.
remote: Counting objects: 100% (40/40), done.
remote: Compressing objects: 100% (28/28), done.
remote: Total 40 (delta 13), reused 30 (delta 8), pack-reused 0
Receiving objects: 100% (40/40), 25.91 KiB | 576.00 KiB/s, done.
Resolving deltas: 100% (13/13), done.

❯ cd projects/lab06
❯ git remote remove origin
❯ git remote add origin git@github.com:${GITHUB_USERNAME}/tp-lab06.git
```

```sh
❯ mkdir third-party                                                                                             
❯ git submodule add https://github.com/google/googletest.git third-party/gtest 
Cloning into 'lab06/third-party/gtest'...
remote: Enumerating objects: 27465, done.
remote: Counting objects: 100% (10/10), done.
remote: Compressing objects: 100% (8/8), done.
remote: Total 27465 (delta 1), reused 6 (delta 1), pack-reused 27455
Receiving objects: 100% (27465/27465), 12.63 MiB | 2.03 MiB/s, done.
Resolving deltas: 100% (20405/20405), done.

❯ cd third-party/gtest && git checkout v1.14.0 && cd ../.. 
Note: switching to 'v1.14.0'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at f8d7d77c Bump version to v1.14 in preparation for release
```

```sh
❯ git add third-party/gtest                                                                                           
❯ git commit -m "added gtest framework" 
[main a9c6a67] added gtest framework
 2 files changed, 4 insertions(+)
 create mode 100644 .gitmodules
 create mode 160000 third-party/gtest
```

```sh                                                                                          
❯ sed -i '/option(BUILD_EXAMPLES "Build examples" OFF)/a\
option(BUILD_TESTS "Build tests" OFF)
' CMakeLists.txt

❯ cat >> CMakeLists.txt <<EOF

if(BUILD_TESTS)
  enable_testing()
  add_subdirectory(third-party/gtest)
  file(GLOB \${PROJECT_NAME}_TEST_SOURCES tests/*.cpp)
  add_executable(check \${\${PROJECT_NAME}_TEST_SOURCES})
  target_link_libraries(check \${PROJECT_NAME} gtest_main)
  add_test(NAME check COMMAND check)
endif()
EOF
```

```sh
❯ mkdir tests                                                                                        
❯ cat > tests/test1.cpp <<EOF
#include <print.hpp>

#include <gtest/gtest.h>

TEST(Print, InFileStream)
{
  std::string filepath = "file.txt";
  std::string text = "hello";
  std::ofstream out{filepath};

  print(text, out);
  out.close();

  std::string result;
  std::ifstream in{filepath};
  in >> result;

  EXPECT_EQ(result, text);
}
EOF
```

```sh
❯ cmake -H. -B_build -DBUILD_TESTS=ON 
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
-- Found Python3: /sbin/python3.12 (found version "3.12.3") found components: Interpreter
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD - Success
-- Found Threads: TRUE
-- Configuring done (1.3s)
-- Generating done (0.0s)
-- Build files have been written to: lab06/_build
```

```sh
❯ cmake --build _build 
[  8%] Building CXX object CMakeFiles/print.dir/sources/print.cpp.o
[ 16%] Linking CXX static library libprint.a
[ 16%] Built target print
[ 25%] Building CXX object third-party/gtest/googletest/CMakeFiles/gtest.dir/src/gtest-all.cc.o
[ 33%] Linking CXX static library ../../../lib/libgtest.a
[ 33%] Built target gtest
[ 41%] Building CXX object third-party/gtest/googletest/CMakeFiles/gtest_main.dir/src/gtest_main.cc.o
[ 50%] Linking CXX static library ../../../lib/libgtest_main.a
[ 50%] Built target gtest_main
[ 58%] Building CXX object CMakeFiles/check.dir/tests/test1.cpp.o
[ 66%] Linking CXX executable check
[ 66%] Built target check
[ 75%] Building CXX object third-party/gtest/googlemock/CMakeFiles/gmock.dir/src/gmock-all.cc.o
[ 83%] Linking CXX static library ../../../lib/libgmock.a
[ 83%] Built target gmock
[ 91%] Building CXX object third-party/gtest/googlemock/CMakeFiles/gmock_main.dir/src/gmock_main.cc.o
[100%] Linking CXX static library ../../../lib/libgmock_main.a
[100%] Built target gmock_main
                                                                          took  8s
❯ cmake --build _build --target test 
Running tests...
Test project lab06/_build
    Start 1: check
1/1 Test #1: check ............................   Passed    0.00 sec

100% tests passed, 0 tests failed out of 1

Total Test time (real) =   0.01 sec
```

```sh
❯ _build/check 
Running main() from lab06/third-party/gtest/googletest/src/gtest_main.cc
[==========] Running 1 test from 1 test suite.
[----------] Global test environment set-up.
[----------] 1 test from Print
[ RUN      ] Print.InFileStream
[       OK ] Print.InFileStream (0 ms)
[----------] 1 test from Print (0 ms total)

[----------] Global test environment tear-down
[==========] 1 test from 1 test suite ran. (0 ms total)
[  PASSED  ] 1 test.
```

```sh
❯ cmake --build _build --target test -- ARGS=--verbose 
Running tests...
UpdateCTestConfiguration  from :lab06/_build/DartConfiguration.tcl
UpdateCTestConfiguration  from :lab06/_build/DartConfiguration.tcl
Test project lab06/_build
Constructing a list of tests
Done constructing a list of tests
Updating test list for fixtures
Added 0 tests to meet fixture requirements
Checking test dependency graph...
Checking test dependency graph end
test 1
    Start 1: check

1: Test command: lab06/_build/check
1: Working Directory: lab06/_build
1: Test timeout computed to be: 10000000
1: Running main() from lab06/third-party/gtest/googletest/src/gtest_main.cc
1: [==========] Running 1 test from 1 test suite.
1: [----------] Global test environment set-up.
1: [----------] 1 test from Print
1: [ RUN      ] Print.InFileStream
1: [       OK ] Print.InFileStream (0 ms)
1: [----------] 1 test from Print (0 ms total)
1: 
1: [----------] Global test environment tear-down
1: [==========] 1 test from 1 test suite ran. (0 ms total)
1: [  PASSED  ] 1 test.
1/1 Test #1: check ............................   Passed    0.01 sec

100% tests passed, 0 tests failed out of 1

Total Test time (real) =   0.01 sec
```

```sh
❯ sed -i 's/lab04/lab06/g' README.md
❯ sed -i 's/\(DCMAKE_INSTALL_PREFIX=_install\)/\1 -DBUILD_TESTS=ON/' .travis.yml 
❯ sed -i '/cmake --build _build --target install/a\
- cmake --build _build --target test -- ARGS=--verbose
' .travis.yml
```

```sh
❯ git add .travis.yml
❯ git add tests
❯ git add -p
diff --git a/CMakeLists.txt b/CMakeLists.txt
index 96a361e..aa7a323 100644
--- a/CMakeLists.txt
+++ b/CMakeLists.txt
@@ -4,6 +4,7 @@ set(CMAKE_CXX_STANDARD 11)
 set(CMAKE_CXX_STANDARD_REQUIRED ON)
 
 option(BUILD_EXAMPLES "Build examples" OFF)
+option(BUILD_TESTS "Build tests" OFF)
 
 project(print)
 
(1/2) Stage this hunk [y,n,q,a,d,j,J,g,/,e,p,?]? ?
y - stage this hunk
n - do not stage this hunk
q - quit; do not stage this hunk or any of the remaining ones
a - stage this hunk and all later hunks in the file
d - do not stage this hunk or any of the later hunks in the file
j - leave this hunk undecided, see next undecided hunk
J - leave this hunk undecided, see next hunk
g - select a hunk to go to
/ - search for a hunk matching the given regex
e - manually edit the current hunk
p - print the current hunk
? - print help
(1/2) Stage this hunk [y,n,q,a,d,j,J,g,/,e,p,?]? p
@@ -4,6 +4,7 @@ set(CMAKE_CXX_STANDARD 11)
 set(CMAKE_CXX_STANDARD_REQUIRED ON)
 
 option(BUILD_EXAMPLES "Build examples" OFF)
+option(BUILD_TESTS "Build tests" OFF)
 
 project(print)
 
(1/2) Stage this hunk [y,n,q,a,d,j,J,g,/,e,p,?]? y
@@ -34,3 +35,12 @@ install(TARGETS print
 
 install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/include/ DESTINATION include)
 install(EXPORT print-config DESTINATION cmake)
+
+if(BUILD_TESTS)
+  enable_testing()
+  add_subdirectory(third-party/gtest)
+  file(GLOB ${PROJECT_NAME}_TEST_SOURCES tests/*.cpp)
+  add_executable(check ${${PROJECT_NAME}_TEST_SOURCES})
+  target_link_libraries(check ${PROJECT_NAME} gtest_main)
+  add_test(NAME check COMMAND check)
+endif()
(2/2) Stage this hunk [y,n,q,a,d,K,g,/,e,p,?]? y

diff --git a/README.md b/README.md
index cd4fca8..8a1d2c9 100644
--- a/README.md
+++ b/README.md
@@ -1,6 +1,6 @@
-[![Build Status](https://app.travis-ci.com/TheIIIrd/lab04.svg?token=gfdgdfgbgcddfdfcdff5&branch=main)](https://app.travis-ci.com/Rigrey/lab04)
+[![Build Status](https://app.travis-ci.com/TheIIIrd/lab06.svg?token=gfdgdfgbgcddfdfcdff5&branch=main)](https://app.travis-ci.com/Rigrey/lab06)
 
-# tp-lab04
+# tp-lab06
 Study of continuous integration systems on the example of Travis CI service.
 
 ## Tutorial
(1/4) Stage this hunk [y,n,q,a,d,j,J,g,/,s,e,p,?]? y
@@ -19,8 +19,8 @@ Study of continuous integration systems on the example of Travis CI service.
 ```
 
 ```sh
-❯ git clone git@github.com:${GITHUB_USERNAME}/tp-lab03.git projects/lab04
-Cloning into 'projects/lab04'...
+❯ git clone git@github.com:${GITHUB_USERNAME}/tp-lab03.git projects/lab06
+Cloning into 'projects/lab06'...
 remote: Enumerating objects: 28, done.
 remote: Counting objects: 100% (28/28), done.
 remote: Compressing objects: 100% (18/18), done.
(2/4) Stage this hunk [y,n,q,a,d,K,j,J,g,/,e,p,?]? y
@@ -28,9 +28,9 @@ remote: Total 28 (delta 7), reused 24 (delta 6), pack-reused 0
 Receiving objects: 100% (28/28), 21.99 KiB | 21.99 MiB/s, done.
 Resolving deltas: 100% (7/7), done.
 
-❯ cd projects/lab04
+❯ cd projects/lab06
 ❯ git remote remove origin
-❯ git remote add origin git@github.com:${GITHUB_USERNAME}/tp-lab04.git
+❯ git remote add origin git@github.com:${GITHUB_USERNAME}/tp-lab06.git
 ```
 
 ```sh
(3/4) Stage this hunk [y,n,q,a,d,K,j,J,g,/,s,e,p,?]? y
@@ -74,6 +74,6 @@ Compressing objects: 100% (3/3), done.
 Writing objects: 100% (3/3), 442 bytes | 442.00 KiB/s, done.
 Total 3 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
 remote: Resolving deltas: 100% (1/1), completed with 1 local object.
-To github.com:TheIIIrd/tp-lab04.git
+To github.com:TheIIIrd/tp-lab06.git
    c7458b7..9320fc2  main -> main

(4/4) Stage this hunk [y,n,q,a,d,K,g,/,e,p,?]? y
 ```

```sh
❯ git push origin main
Enumerating objects: 44, done.
Counting objects: 100% (44/44), done.
Delta compression using up to 4 threads
Compressing objects: 100% (26/26), done.
Writing objects: 100% (44/44), 26.29 KiB | 26.29 MiB/s, done.
Total 44 (delta 14), reused 39 (delta 13), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (14/14), done.
To github.com:TheIIIrd/tp-lab06.git
 * [new branch]      main -> main
```
