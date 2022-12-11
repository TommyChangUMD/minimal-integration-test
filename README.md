A simple method to test ROS nodes using gtest and a minimalist
approach to launching ROS nodes.

First, move this directory to the `src/` folder of your colcon
workspace.  This is *important* or your unit test will get a lot of
errors from `ament_lint_cmake`.


## How to Compile:
```
rm -rf build/minimal_integration_test  # if needed
colcon build --packages-select minimal_integration_test
```

## How to Run:
First, soruce the setup file:
```
source install/setup.bash
```
### then, run the test and look at the output:
```
colcon test --packages-select minimal_integration_test
cat log/latest_test/minimal_integration_test/stdout_stderr.log
```

### check the return status:
```
colcon test-result --test-result-base build/minimal_integration_test
echo $?
```

## Example output

```
integration_test_test.gtest.xml
1: [==========] Running 1 test from 1 test suite.
1: [----------] Global test environment set-up.
1: [----------] 1 test from TaskPlanningFixture
1: [ RUN      ] TaskPlanningFixture.TrueIsTrueTest
1: [INFO] [1670714981.602751739] [basic_test]: DONE WITH CONSTRUCTOR!!
1: [INFO] [1670714983.518949944] [basic_test]: DONE WITH SETUP!!
1: TEST BEGINNING!!
1: [INFO] [1670714984.020363253] [basic_test]: I heard: 'Hello, world! 3'
1: [INFO] [1670714984.520346579] [basic_test]: I heard: 'Hello, world! 4'
1: [INFO] [1670714985.020349886] [basic_test]: I heard: 'Hello, world! 5'
1: [INFO] [1670714985.520312969] [basic_test]: I heard: 'Hello, world! 6'
1: [INFO] [1670714986.020314111] [basic_test]: I heard: 'Hello, world! 7'
1: DONE WITH TEARDOWN
1: [       OK ] TaskPlanningFixture.TrueIsTrueTest (4978 ms)
1: [----------] 1 test from TaskPlanningFixture (4978 ms total)
1: 
1: [----------] Global test environment tear-down
1: [==========] 1 test from 1 test suite ran. (4979 ms total)
1: [  PASSED  ] 1 test.
1: DONE SHUTTING DOWN ROS

...

Label Time Summary:
cppcheck      =   0.19 sec*proc (1 test)
gtest         =   5.19 sec*proc (1 test)
lint_cmake    =   0.17 sec*proc (1 test)
linter        =   0.73 sec*proc (3 tests)
xmllint       =   0.36 sec*proc (1 test)

```
