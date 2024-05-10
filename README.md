[![Build Status](https://app.travis-ci.com/Rigrey/lab04.svg?token=sSjKqXpxzeqqaxAwq5f2&branch=main)](https://app.travis-ci.com/Rigrey/lab04)

# tp-lab07
A study of package management systems using Hunter as an example.

## Tutorial

```sh
❯ export GITHUB_USERNAME=TheIIIrd
❯ alias gsed=sed
```

```sh
❯ cd ${GITHUB_USERNAME}/workspace
❯ pushd .
~/TheIIIrd/workspace ~/TheIIIrd/workspace

❯ source scripts/activate
```

```sh
❯ git clone git@github.com:${GITHUB_USERNAME}/tp-lab06.git projects/lab07
Cloning into 'projects/lab07'...
remote: Enumerating objects: 66, done.
remote: Counting objects: 100% (66/66), done.
remote: Compressing objects: 100% (42/42), done.
remote: Total 66 (delta 24), reused 53 (delta 19), pack-reused 0
Receiving objects: 100% (66/66), 37.73 KiB | 386.00 KiB/s, done.
Resolving deltas: 100% (24/24), done.

❯ cd projects/lab07
❯ git remote remove origin
❯ git remote add origin https://github.com/${GITHUB_USERNAME}/lab07
```

```sh
❯ mkdir -p cmake
❯ wget https://raw.githubusercontent.com/cpp-pm/gate/master/cmake/HunterGate.cmake -O cmake/HunterGate.cmake
--2024-05-10 09:03:09--  https://raw.githubusercontent.com/cpp-pm/gate/master/cmake/HunterGate.cmake
Loaded CA certificate '/etc/ssl/certs/ca-certificates.crt'
Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 185.199.110.133, 185.199.109.133, 185.199.108.133, ...
Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|185.199.110.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 17227 (17K) [text/plain]
Saving to: ‘cmake/HunterGate.cmake’

cmake/HunterGate.cmake              100%[================================================================>]  16.82K  --.-KB/s    in 0.002s  

2024-05-10 09:03:10 (8.58 MB/s) - ‘cmake/HunterGate.cmake’ saved [17227/17227]
```

```sh
❯ nvim CMakeLists.txt
❯ git rm -rf third-party/gtest 
rm 'third-party/gtest'
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
❯ cmake -H. -B_builds -DBUILD_TESTS=ON 
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- The C compiler identification is GNU 14.1.1
-- The CXX compiler identification is GNU 14.1.1
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
-- [hunter] Calculating Toolchain-SHA1
-- [hunter] Calculating Config-SHA1
-- [hunter] HUNTER_ROOT: .hunter
-- [hunter] [ Hunter-ID: a20151e | Toolchain-ID: bfeb507 | Config-ID: 4abab25 ]
-- [hunter] GTEST_ROOT: .hunter/_Base/a20151e/bfeb507/4abab25/Install (ver.: 1.14.0)
-- [hunter] Building GTest
loading initial cache file .hunter/_Base/a20151e/bfeb507/4abab25/cache.cmake
loading initial cache file .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/args.cmake
-- The C compiler identification is GNU 14.1.1
-- The CXX compiler identification is GNU 14.1.1
-- Check for working C compiler: /sbin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /sbin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done (0.1s)
-- Generating done (0.0s)
-- Build files have been written to: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Build
[  6%] Creating directories for 'GTest-Release'
[ 12%] Performing download step (download, verify and extract) for 'GTest-Release'
-- verifying file...
       file='.hunter/_Base/Download/GTest/1.14.0/2b28c2a/v1.14.0.tar.gz'
-- File already exists and hash match (skip download):
  file='.hunter/_Base/Download/GTest/1.14.0/2b28c2a/v1.14.0.tar.gz'
  SHA1='2b28c2a3a30d86b1759543ef61fac3c4d69f8c4c'
-- extracting...
     src='.hunter/_Base/Download/GTest/1.14.0/2b28c2a/v1.14.0.tar.gz'
     dst='.hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Source'
-- extracting... [tar xfz]
-- extracting... [analysis]
-- extracting... [rename]
-- extracting... [clean up]
-- extracting... done
[ 18%] No update step for 'GTest-Release'
[ 25%] No patch step for 'GTest-Release'
[ 31%] Performing configure step for 'GTest-Release'
loading initial cache file .hunter/_Base/a20151e/bfeb507/4abab25/cache.cmake
loading initial cache file .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/args.cmake
-- The C compiler identification is GNU 14.1.1
-- The CXX compiler identification is GNU 14.1.1
-- Check for working C compiler: /sbin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /sbin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Found Python3: /sbin/python3.12 (found version "3.12.3") found components: Interpreter
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD - Success
-- Found Threads: TRUE
-- Configuring done (0.4s)
-- Generating done (0.0s)
-- Build files have been written to: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Build/GTest-Release-prefix/src/GTest-Release-build
[ 37%] Performing build step for 'GTest-Release'
[ 12%] Building CXX object googletest/CMakeFiles/gtest.dir/src/gtest-all.cc.o
[ 25%] Linking CXX static library ../lib/libgtest.a
[ 25%] Built target gtest
[ 50%] Building CXX object googlemock/CMakeFiles/gmock.dir/src/gmock-all.cc.o
[ 50%] Building CXX object googletest/CMakeFiles/gtest_main.dir/src/gtest_main.cc.o
[ 62%] Linking CXX static library ../lib/libgtest_main.a
[ 62%] Built target gtest_main
[ 75%] Linking CXX static library ../lib/libgmock.a
[ 75%] Built target gmock
[ 87%] Building CXX object googlemock/CMakeFiles/gmock_main.dir/src/gmock_main.cc.o
[100%] Linking CXX static library ../lib/libgmock_main.a
[100%] Built target gmock_main
[ 43%] Performing install step for 'GTest-Release'
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gmock
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gmock/gmock-actions.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gmock/gmock-cardinalities.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gmock/gmock-function-mocker.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gmock/gmock-matchers.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gmock/gmock-more-actions.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gmock/gmock-more-matchers.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gmock/gmock-nice-strict.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gmock/gmock-spec-builders.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gmock/gmock.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gmock/internal
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gmock/internal/custom
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gmock/internal/custom/README.md
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gmock/internal/custom/gmock-generated-actions.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gmock/internal/custom/gmock-matchers.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gmock/internal/custom/gmock-port.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gmock/internal/gmock-internal-utils.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gmock/internal/gmock-port.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gmock/internal/gmock-pp.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/lib/libgmock.a
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/lib/libgmock_main.a
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/lib/pkgconfig/gmock.pc
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/lib/pkgconfig/gmock_main.pc
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/lib/cmake/GTest/GTestTargets.cmake
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/lib/cmake/GTest/GTestTargets-release.cmake
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/lib/cmake/GTest/GTestConfigVersion.cmake
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/lib/cmake/GTest/GTestConfig.cmake
-- Up-to-date: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/gtest-assertion-result.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/gtest-death-test.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/gtest-matchers.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/gtest-message.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/gtest-param-test.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/gtest-printers.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/gtest-spi.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/gtest-test-part.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/gtest-typed-test.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/gtest.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/gtest_pred_impl.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/gtest_prod.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/internal
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/internal/custom
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/internal/custom/README.md
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/internal/custom/gtest-port.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/internal/custom/gtest-printers.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/internal/custom/gtest.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/internal/gtest-death-test-internal.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/internal/gtest-filepath.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/internal/gtest-internal.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/internal/gtest-param-util.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/internal/gtest-port-arch.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/internal/gtest-port.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/internal/gtest-string.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/internal/gtest-type-util.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/lib/libgtest.a
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/lib/libgtest_main.a
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/lib/pkgconfig/gtest.pc
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/lib/pkgconfig/gtest_main.pc
loading initial cache file .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/args.cmake
[ 50%] Completed 'GTest-Release'
[ 50%] Built target GTest-Release
[ 56%] Creating directories for 'GTest-Debug'
[ 62%] Performing download step (download, verify and extract) for 'GTest-Debug'
-- verifying file...
       file='.hunter/_Base/Download/GTest/1.14.0/2b28c2a/v1.14.0.tar.gz'
-- File already exists and hash match (skip download):
  file='.hunter/_Base/Download/GTest/1.14.0/2b28c2a/v1.14.0.tar.gz'
  SHA1='2b28c2a3a30d86b1759543ef61fac3c4d69f8c4c'
-- extracting...
     src='.hunter/_Base/Download/GTest/1.14.0/2b28c2a/v1.14.0.tar.gz'
     dst='.hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Source'
-- extracting... [tar xfz]
-- extracting... [analysis]
-- extracting... [rename]
-- extracting... [clean up]
-- extracting... done
[ 68%] No update step for 'GTest-Debug'
[ 75%] No patch step for 'GTest-Debug'
[ 81%] Performing configure step for 'GTest-Debug'
loading initial cache file .hunter/_Base/a20151e/bfeb507/4abab25/cache.cmake
loading initial cache file .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/args.cmake
-- The C compiler identification is GNU 14.1.1
-- The CXX compiler identification is GNU 14.1.1
-- Check for working C compiler: /sbin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /sbin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Found Python3: /sbin/python3.12 (found version "3.12.3") found components: Interpreter
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD - Success
-- Found Threads: TRUE
-- Configuring done (0.4s)
-- Generating done (0.0s)
-- Build files have been written to: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Build/GTest-Debug-prefix/src/GTest-Debug-build
[ 87%] Performing build step for 'GTest-Debug'
[ 12%] Building CXX object googletest/CMakeFiles/gtest.dir/src/gtest-all.cc.o
[ 25%] Linking CXX static library ../lib/libgtestd.a
[ 25%] Built target gtest
[ 37%] Building CXX object googletest/CMakeFiles/gtest_main.dir/src/gtest_main.cc.o
[ 50%] Building CXX object googlemock/CMakeFiles/gmock.dir/src/gmock-all.cc.o
[ 62%] Linking CXX static library ../lib/libgtest_maind.a
[ 62%] Built target gtest_main
[ 75%] Linking CXX static library ../lib/libgmockd.a
[ 75%] Built target gmock
[ 87%] Building CXX object googlemock/CMakeFiles/gmock_main.dir/src/gmock_main.cc.o
[100%] Linking CXX static library ../lib/libgmock_maind.a
[100%] Built target gmock_main
[ 93%] Performing install step for 'GTest-Debug'
-- Up-to-date: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include
-- Up-to-date: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gmock
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gmock/gmock-actions.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gmock/gmock-cardinalities.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gmock/gmock-function-mocker.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gmock/gmock-matchers.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gmock/gmock-more-actions.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gmock/gmock-more-matchers.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gmock/gmock-nice-strict.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gmock/gmock-spec-builders.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gmock/gmock.h
-- Up-to-date: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gmock/internal
-- Up-to-date: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gmock/internal/custom
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gmock/internal/custom/README.md
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gmock/internal/custom/gmock-generated-actions.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gmock/internal/custom/gmock-matchers.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gmock/internal/custom/gmock-port.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gmock/internal/gmock-internal-utils.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gmock/internal/gmock-port.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gmock/internal/gmock-pp.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/lib/libgmockd.a
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/lib/libgmock_maind.a
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/lib/pkgconfig/gmock.pc
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/lib/pkgconfig/gmock_main.pc
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/lib/cmake/GTest/GTestTargets.cmake
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/lib/cmake/GTest/GTestTargets-debug.cmake
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/lib/cmake/GTest/GTestConfigVersion.cmake
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/lib/cmake/GTest/GTestConfig.cmake
-- Up-to-date: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include
-- Up-to-date: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/gtest-assertion-result.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/gtest-death-test.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/gtest-matchers.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/gtest-message.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/gtest-param-test.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/gtest-printers.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/gtest-spi.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/gtest-test-part.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/gtest-typed-test.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/gtest.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/gtest_pred_impl.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/gtest_prod.h
-- Up-to-date: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/internal
-- Up-to-date: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/internal/custom
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/internal/custom/README.md
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/internal/custom/gtest-port.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/internal/custom/gtest-printers.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/internal/custom/gtest.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/internal/gtest-death-test-internal.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/internal/gtest-filepath.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/internal/gtest-internal.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/internal/gtest-param-util.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/internal/gtest-port-arch.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/internal/gtest-port.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/internal/gtest-string.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/include/gtest/internal/gtest-type-util.h
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/lib/libgtestd.a
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/lib/libgtest_maind.a
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/lib/pkgconfig/gtest.pc
-- Installing: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/Install/lib/pkgconfig/gtest_main.pc
loading initial cache file .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest/args.cmake
[100%] Completed 'GTest-Debug'
[100%] Built target GTest-Debug
-- [hunter] Build step successful (dir: .hunter/_Base/a20151e/bfeb507/4abab25/Build/GTest)
-- [hunter] Cache saved: .hunter/_Base/Cache/raw/2868dce809e469adf79a8f821fbba2e5fa60b198.tar.bz2
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD - Success
-- Found Threads: TRUE
-- Configuring done (20.0s)
-- Generating done (0.0s)
-- Build files have been written to: lab07/_builds
```

```sh
❯ cmake --build _builds
[ 25%] Building CXX object CMakeFiles/print.dir/sources/print.cpp.o
[ 50%] Linking CXX static library libprint.a
[ 50%] Built target print
[ 75%] Building CXX object CMakeFiles/check.dir/tests/test1.cpp.o
[100%] Linking CXX executable check
[100%] Built target check

❯ cmake --build _builds --target test
Running tests...
Test project Projects/TIMP/Workbench/lab07/_builds
    Start 1: check
1/1 Test #1: check ............................   Passed    0.00 sec

100% tests passed, 0 tests failed out of 1

Total Test time (real) =   0.00 sec
```

```sh
❯ ls -la $HOME/.hunter 
total 0
drwxr-xr-x 1 user user  10 May  6 12:26 .
drwx------ 1 user user 576 May 10 09:46 ..
drwxr-xr-x 1 user user  66 May 10 09:15 _Base
```

```sh
❯ mkdir demo 
❯ cat > demo/main.cpp <<EOF
#include <print.hpp>

#include <cstdlib>

int main(int argc, char* argv[])
{
  const char* log_path = std::getenv("LOG_PATH");
  if (log_path == nullptr)
  {
    std::cerr << "undefined environment variable: LOG_PATH" << std::endl;
    return 1;
  }
  std::string text;
  while (std::cin >> text)
  {
    std::ofstream out{log_path, std::ios_base::app};
    print(text, out);
    out << std::endl;
  }
}
EOF

❯ nvim CMakeLists.txt
```

```sh
❯ mkdir tools 
❯ git submodule add https://github.com/ruslo/polly tools/polly
Cloning into 'Projects/TIMP/Workbench/lab07/tools/polly'...
remote: Enumerating objects: 6578, done.
remote: Counting objects: 100% (32/32), done.
remote: Compressing objects: 100% (15/15), done.
remote: Total 6578 (delta 21), reused 20 (delta 17), pack-reused 6546
Receiving objects: 100% (6578/6578), 1.68 MiB | 944.00 KiB/s, done.
Resolving deltas: 100% (4551/4551), done.
```

```sh
❯ tools/polly/bin/polly.py --test 
Python version: 3.12
Build dir: Projects/TIMP/Workbench/lab07/_builds/default
Execute command: [
  `which`
  `cmake`
]

[Projects/TIMP/Workbench/lab07]> "which" "cmake"

/sbin/cmake
Execute command: [
  `cmake`
  `--version`
]

[Projects/TIMP/Workbench/lab07]> "cmake" "--version"

cmake version 3.29.3

CMake suite maintained and supported by Kitware (kitware.com/cmake).
Execute command: [
  `cmake`
  `-H.`
  `-BProjects/TIMP/Workbench/lab07/_builds/default`
  `-DCMAKE_TOOLCHAIN_FILE=Projects/TIMP/Workbench/lab07/tools/polly/default.cmake`
]

[Projects/TIMP/Workbench/lab07]> "cmake" "-H." "-BProjects/TIMP/Workbench/lab07/_builds/default" "-DCMAKE_TOOLCHAIN_FILE=Projects/TIMP/Workbench/lab07/tools/polly/default.cmake"

CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- [polly] Used toolchain: Default
-- The C compiler identification is GNU 14.1.1
-- The CXX compiler identification is GNU 14.1.1
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
-- [hunter] Calculating Toolchain-SHA1
-- [hunter] Calculating Config-SHA1
-- [hunter] HUNTER_ROOT: .hunter
-- [hunter] [ Hunter-ID: a20151e | Toolchain-ID: bfeb507 | Config-ID: 4abab25 ]
-- [hunter] GTEST_ROOT: .hunter/_Base/a20151e/bfeb507/4abab25/Install (ver.: 1.14.0)
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD - Success
-- Found Threads: TRUE
-- Configuring done (0.9s)
-- Generating done (0.0s)
-- Build files have been written to: Projects/TIMP/Workbench/lab07/_builds/default
Execute command: [
  `cmake`
  `--build`
  `Projects/TIMP/Workbench/lab07/_builds/default`
  `--`
]

[Projects/TIMP/Workbench/lab07]> "cmake" "--build" "Projects/TIMP/Workbench/lab07/_builds/default" "--"

[ 25%] Building CXX object CMakeFiles/print.dir/sources/print.cpp.o
[ 50%] Linking CXX static library libprint.a
[ 50%] Built target print
[ 75%] Building CXX object CMakeFiles/demo.dir/demo/main.cpp.o
[100%] Linking CXX executable demo
[100%] Built target demo
Run tests
Execute command: [
  `ctest`
]

[Projects/TIMP/Workbench/lab07/_builds/default]> "ctest"

*********************************
No test configuration file found!
*********************************
Usage

  ctest [options]

-
Log saved: Projects/TIMP/Workbench/lab07/_logs/polly/default/log.txt
-
Generate: 0:00:01.869441s
Build: 0:00:01.469534s
Test: 0:00:00.012114s
-
Total: 0:00:03.351290s
-
SUCCESS
```

```sh
❯ tools/polly/bin/polly.py --toolchain clang-cxx14 
Python version: 3.12
Build dir: Projects/TIMP/Workbench/lab07/_builds/clang-cxx14
Execute command: [
  `which`
  `cmake`
]

[Projects/TIMP/Workbench/lab07]> "which" "cmake"

/sbin/cmake
Execute command: [
  `cmake`
  `--version`
]

[Projects/TIMP/Workbench/lab07]> "cmake" "--version"

cmake version 3.29.3

CMake suite maintained and supported by Kitware (kitware.com/cmake).
Execute command: [
  `cmake`
  `-H.`
  `-BProjects/TIMP/Workbench/lab07/_builds/clang-cxx14`
  `-GUnix Makefiles`
  `-DCMAKE_TOOLCHAIN_FILE=Projects/TIMP/Workbench/lab07/tools/polly/clang-cxx14.cmake`
]

[Projects/TIMP/Workbench/lab07]> "cmake" "-H." "-BProjects/TIMP/Workbench/lab07/_builds/clang-cxx14" "-GUnix Makefiles" "-DCMAKE_TOOLCHAIN_FILE=Projects/TIMP/Workbench/lab07/tools/polly/clang-cxx14.cmake"

CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- [polly] Used toolchain: clang / c++14 support
-- The C compiler identification is Clang 17.0.6
-- The CXX compiler identification is Clang 17.0.6
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /sbin/clang - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /sbin/clang++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- [hunter] Calculating Toolchain-SHA1
-- [hunter] Calculating Config-SHA1
-- [hunter] HUNTER_ROOT: .hunter
-- [hunter] [ Hunter-ID: a20151e | Toolchain-ID: 55ff7a0 | Config-ID: 4abab25 ]
-- [hunter] GTEST_ROOT: .hunter/_Base/a20151e/55ff7a0/4abab25/Install (ver.: 1.14.0)
-- [hunter] Building GTest
loading initial cache file .hunter/_Base/a20151e/55ff7a0/4abab25/cache.cmake
loading initial cache file .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/args.cmake
-- [polly] Used toolchain: clang / c++14 support
-- The C compiler identification is Clang 17.0.6
-- The CXX compiler identification is Clang 17.0.6
-- Check for working C compiler: /sbin/clang - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /sbin/clang++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done (0.2s)
-- Generating done (0.0s)
-- Build files have been written to: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Build
[  6%] Creating directories for 'GTest-Release'
[ 12%] Performing download step (download, verify and extract) for 'GTest-Release'
-- verifying file...
       file='.hunter/_Base/Download/GTest/1.14.0/2b28c2a/v1.14.0.tar.gz'
-- File already exists and hash match (skip download):
  file='.hunter/_Base/Download/GTest/1.14.0/2b28c2a/v1.14.0.tar.gz'
  SHA1='2b28c2a3a30d86b1759543ef61fac3c4d69f8c4c'
-- extracting...
     src='.hunter/_Base/Download/GTest/1.14.0/2b28c2a/v1.14.0.tar.gz'
     dst='.hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Source'
-- extracting... [tar xfz]
-- extracting... [analysis]
-- extracting... [rename]
-- extracting... [clean up]
-- extracting... done
[ 18%] No update step for 'GTest-Release'
[ 25%] No patch step for 'GTest-Release'
[ 31%] Performing configure step for 'GTest-Release'
loading initial cache file .hunter/_Base/a20151e/55ff7a0/4abab25/cache.cmake
loading initial cache file .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/args.cmake
-- [polly] Used toolchain: clang / c++14 support
-- The C compiler identification is Clang 17.0.6
-- The CXX compiler identification is Clang 17.0.6
-- Check for working C compiler: /sbin/clang - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /sbin/clang++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Found Python3: /sbin/python3.12 (found version "3.12.3") found components: Interpreter
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD - Success
-- Found Threads: TRUE
-- Configuring done (0.4s)
-- Generating done (0.0s)
-- Build files have been written to: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Build/GTest-Release-prefix/src/GTest-Release-build
[ 37%] Performing build step for 'GTest-Release'
[ 12%] Building CXX object googletest/CMakeFiles/gtest.dir/src/gtest-all.cc.o
[ 25%] Linking CXX static library ../lib/libgtest.a
[ 25%] Built target gtest
[ 50%] Building CXX object googlemock/CMakeFiles/gmock.dir/src/gmock-all.cc.o
[ 50%] Building CXX object googletest/CMakeFiles/gtest_main.dir/src/gtest_main.cc.o
[ 62%] Linking CXX static library ../lib/libgtest_main.a
[ 62%] Built target gtest_main
[ 75%] Linking CXX static library ../lib/libgmock.a
[ 75%] Built target gmock
[ 87%] Building CXX object googlemock/CMakeFiles/gmock_main.dir/src/gmock_main.cc.o
[100%] Linking CXX static library ../lib/libgmock_main.a
[100%] Built target gmock_main
[ 43%] Performing install step for 'GTest-Release'
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gmock
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gmock/gmock-actions.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gmock/gmock-cardinalities.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gmock/gmock-function-mocker.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gmock/gmock-matchers.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gmock/gmock-more-actions.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gmock/gmock-more-matchers.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gmock/gmock-nice-strict.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gmock/gmock-spec-builders.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gmock/gmock.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gmock/internal
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gmock/internal/custom
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gmock/internal/custom/README.md
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gmock/internal/custom/gmock-generated-actions.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gmock/internal/custom/gmock-matchers.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gmock/internal/custom/gmock-port.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gmock/internal/gmock-internal-utils.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gmock/internal/gmock-port.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gmock/internal/gmock-pp.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/lib/libgmock.a
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/lib/libgmock_main.a
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/lib/pkgconfig/gmock.pc
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/lib/pkgconfig/gmock_main.pc
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/lib/cmake/GTest/GTestTargets.cmake
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/lib/cmake/GTest/GTestTargets-release.cmake
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/lib/cmake/GTest/GTestConfigVersion.cmake
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/lib/cmake/GTest/GTestConfig.cmake
-- Up-to-date: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/gtest-assertion-result.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/gtest-death-test.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/gtest-matchers.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/gtest-message.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/gtest-param-test.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/gtest-printers.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/gtest-spi.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/gtest-test-part.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/gtest-typed-test.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/gtest.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/gtest_pred_impl.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/gtest_prod.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/internal
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/internal/custom
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/internal/custom/README.md
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/internal/custom/gtest-port.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/internal/custom/gtest-printers.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/internal/custom/gtest.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/internal/gtest-death-test-internal.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/internal/gtest-filepath.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/internal/gtest-internal.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/internal/gtest-param-util.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/internal/gtest-port-arch.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/internal/gtest-port.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/internal/gtest-string.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/internal/gtest-type-util.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/lib/libgtest.a
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/lib/libgtest_main.a
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/lib/pkgconfig/gtest.pc
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/lib/pkgconfig/gtest_main.pc
loading initial cache file .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/args.cmake
[ 50%] Completed 'GTest-Release'
[ 50%] Built target GTest-Release
[ 56%] Creating directories for 'GTest-Debug'
[ 62%] Performing download step (download, verify and extract) for 'GTest-Debug'
-- verifying file...
       file='.hunter/_Base/Download/GTest/1.14.0/2b28c2a/v1.14.0.tar.gz'
-- File already exists and hash match (skip download):
  file='.hunter/_Base/Download/GTest/1.14.0/2b28c2a/v1.14.0.tar.gz'
  SHA1='2b28c2a3a30d86b1759543ef61fac3c4d69f8c4c'
-- extracting...
     src='.hunter/_Base/Download/GTest/1.14.0/2b28c2a/v1.14.0.tar.gz'
     dst='.hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Source'
-- extracting... [tar xfz]
-- extracting... [analysis]
-- extracting... [rename]
-- extracting... [clean up]
-- extracting... done
[ 68%] No update step for 'GTest-Debug'
[ 75%] No patch step for 'GTest-Debug'
[ 81%] Performing configure step for 'GTest-Debug'
loading initial cache file .hunter/_Base/a20151e/55ff7a0/4abab25/cache.cmake
loading initial cache file .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/args.cmake
-- [polly] Used toolchain: clang / c++14 support
-- The C compiler identification is Clang 17.0.6
-- The CXX compiler identification is Clang 17.0.6
-- Check for working C compiler: /sbin/clang - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /sbin/clang++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Found Python3: /sbin/python3.12 (found version "3.12.3") found components: Interpreter
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD - Success
-- Found Threads: TRUE
-- Configuring done (0.5s)
-- Generating done (0.0s)
-- Build files have been written to: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Build/GTest-Debug-prefix/src/GTest-Debug-build
[ 87%] Performing build step for 'GTest-Debug'
[ 12%] Building CXX object googletest/CMakeFiles/gtest.dir/src/gtest-all.cc.o
[ 25%] Linking CXX static library ../lib/libgtestd.a
[ 25%] Built target gtest
[ 50%] Building CXX object googletest/CMakeFiles/gtest_main.dir/src/gtest_main.cc.o
[ 50%] Building CXX object googlemock/CMakeFiles/gmock.dir/src/gmock-all.cc.o
[ 62%] Linking CXX static library ../lib/libgtest_maind.a
[ 62%] Built target gtest_main
[ 75%] Linking CXX static library ../lib/libgmockd.a
[ 75%] Built target gmock
[ 87%] Building CXX object googlemock/CMakeFiles/gmock_main.dir/src/gmock_main.cc.o
[100%] Linking CXX static library ../lib/libgmock_maind.a
[100%] Built target gmock_main
[ 93%] Performing install step for 'GTest-Debug'
-- Up-to-date: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include
-- Up-to-date: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gmock
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gmock/gmock-actions.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gmock/gmock-cardinalities.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gmock/gmock-function-mocker.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gmock/gmock-matchers.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gmock/gmock-more-actions.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gmock/gmock-more-matchers.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gmock/gmock-nice-strict.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gmock/gmock-spec-builders.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gmock/gmock.h
-- Up-to-date: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gmock/internal
-- Up-to-date: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gmock/internal/custom
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gmock/internal/custom/README.md
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gmock/internal/custom/gmock-generated-actions.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gmock/internal/custom/gmock-matchers.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gmock/internal/custom/gmock-port.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gmock/internal/gmock-internal-utils.h
.hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gmock/internal/gmock-port.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gmock/internal/gmock-pp.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/lib/libgmockd.a
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/lib/libgmock_maind.a
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/lib/pkgconfig/gmock.pc
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/lib/pkgconfig/gmock_main.pc
.hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/lib/cmake/GTest/GTestTargets.cmake
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/lib/cmake/GTest/GTestTargets-debug.cmake
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/lib/cmake/GTest/GTestConfigVersion.cmake
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/lib/cmake/GTest/GTestConfig.cmake
-- Up-to-date: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include
-- Up-to-date: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/gtest-assertion-result.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/gtest-death-test.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/gtest-matchers.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/gtest-message.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/gtest-param-test.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/gtest-printers.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/gtest-spi.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/gtest-test-part.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/gtest-typed-test.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/gtest.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/gtest_pred_impl.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/gtest_prod.h
-- Up-to-date: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/internal
-- Up-to-date: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/internal/custom
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/internal/custom/README.md
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/internal/custom/gtest-port.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/internal/custom/gtest-printers.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/internal/custom/gtest.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/internal/gtest-death-test-internal.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/internal/gtest-filepath.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/internal/gtest-internal.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/internal/gtest-param-util.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/internal/gtest-port-arch.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/internal/gtest-port.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/internal/gtest-string.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/include/gtest/internal/gtest-type-util.h
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/lib/libgtestd.a
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/lib/libgtest_maind.a
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/lib/pkgconfig/gtest.pc
-- Installing: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/Install/lib/pkgconfig/gtest_main.pc
loading initial cache file .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest/args.cmake
[100%] Completed 'GTest-Debug'
[100%] Built target GTest-Debug
-- [hunter] Build step successful (dir: .hunter/_Base/a20151e/55ff7a0/4abab25/Build/GTest)
-- [hunter] Cache saved: .hunter/_Base/Cache/raw/90ce999c9a8b42022d9d76b655526430806a0a04.tar.bz2
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD - Success
-- Found Threads: TRUE
-- Configuring done (15.8s)
-- Generating done (0.0s)
-- Build files have been written to: Projects/TIMP/Workbench/lab07/_builds/clang-cxx14
Execute command: [
  `cmake`
  `--build`
  `Projects/TIMP/Workbench/lab07/_builds/clang-cxx14`
  `--`
]

[Projects/TIMP/Workbench/lab07]> "cmake" "--build" "Projects/TIMP/Workbench/lab07/_builds/clang-cxx14" "--"

[ 25%] Building CXX object CMakeFiles/print.dir/sources/print.cpp.o
[ 50%] Linking CXX static library libprint.a
[ 50%] Built target print
[ 75%] Building CXX object CMakeFiles/demo.dir/demo/main.cpp.o
[100%] Linking CXX executable demo
[100%] Built target demo
-
Log saved: Projects/TIMP/Workbench/lab07/_logs/polly/clang-cxx14/log.txt
-
Generate: 0:00:16.830440s
Build: 0:00:01.529244s
-
Total: 0:00:18.360002s
-
SUCCESS
```

```sh
❯ git add .                                                    
❯ git commit -m "Added and configured Hunter"         
[main 769c333] Added and configured Hunter
 7 files changed, 608 insertions(+), 4 deletions(-)
 create mode 100644 cmake/HunterGate.cmake
 create mode 100644 demo/main.cpp
 create mode 100644 tests/test1.cpp
 delete mode 160000 third-party/gtest
 create mode 160000 tools/polly

❯ git push origin main
Enumerating objects: 77, done.
Counting objects: 100% (77/77), done.
Delta compression using up to 4 threads
Compressing objects: 100% (44/44), done.
Writing objects: 100% (77/77), 43.90 KiB | 43.90 MiB/s, done.
Total 77 (delta 26), reused 64 (delta 24), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (26/26), done.
To github.com:TheIIIrd/tp-lab07.git
 * [new branch]      main -> main
```
