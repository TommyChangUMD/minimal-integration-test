A simple method to test ROS nodes using gtest and a minimalist
approach to launching ROS nodes.  Note: The integration test used in
this example is purposely kept simple.  It makes system() calls with
the following assumption:

  - Linux OS
  - pkill command


First, move this directory to the `src/` folder of your colcon
workspace.  This is *important* or your unit test will get a lot of
errors from `ament_lint_cmake`.

For example, your workspace directory structure should look like this:

```
colcon_ws/
├── build/
├── install/
├── log/
└── src/
    ├── minimal-integration-test/
    ├── ros_package1/
    ├── ros_package2/
    └── ros_package3/
```

``` bash
mkdir -p ~/colcon_ws/src
cd ~/colcon_ws/src
git clone https://github.com/TommyChangUMD/minimal-integration-test.git
```

## How to Compile:
```bash
cd ~/colcon_ws/   # assuming your workspace is at '~/colcon_ws'
rm -rf install/ build/
source /opt/ros/humble/setup.bash  # if needed
colcon build 
```

## How to Run:
First, soruce the setup file:
```bash
source install/setup.bash
```
### then, run the test and look at the output:
```bash
colcon test 
cat log/latest_test/minimal_integration_test/stdout_stderr.log
```

### check the return status:
```
colcon test-result --verbose --test-result-base build/minimal_integration_test
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

... <SKIP> ...

Label Time Summary:
cppcheck      =   0.19 sec*proc (1 test)
gtest         =   5.19 sec*proc (1 test)
lint_cmake    =   0.17 sec*proc (1 test)
linter        =   0.73 sec*proc (3 tests)
xmllint       =   0.36 sec*proc (1 test)

```
