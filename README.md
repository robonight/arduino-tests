# robonight

## quickstart

```sh
pushd arduino-gmock-sample && docker run -it -v $(pwd):/arduino/project mkainer/arduino-test && popd
```

## more elaborate

This docker image can run [ikeyasu/arduino-mock](https://github.com/ikeyasu/arduino-mock) tests in a docker image. To run them, you'll need the following structure:

```sh
├── yourapplication
│   ├── yourapplication.ino
│   └── test
│       ├── CMakeLists.txt
│       ├── your_unittest.cc
│       └── test_all.cc
```

How you name yourproject, the ino file or the unittests is up to you, as well as how many files you have. `test_all.cc` and CMakeLists.txt have to be there. The CmakeLists.txt file should be empty, the test_all.cc should contain the following content:

```cc
#include "your_unittest.cc"

int main(int argc, char* argv[]) {
  ::testing::InitGoogleTest(&argc, argv);
  return RUN_ALL_TESTS();
}
```

In the unittest file you can reference gtest and arduino-mock as you would with the project running on your machine. 

Then run the unittests with 

```
docker run -it -v $(pwd):/arduino/project mkainer/arduino-test
```

## building the container yourself

You can build your own `arduino-test` container with 

```
pushd arduino-tests && docker build --tag arduino-test . && popd 
```
