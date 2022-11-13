
## How to Compile:
```
colcon build --packages-select minimal_integration_test
```

## How to Run:
### without verbose output:
```
colcon test --packages-select minimal_integration_test
```  
### with verbose output:
```
colcon test --event-handlers console_direct+ --packages-select minimal_integration_test
```
### check the return status:
```
colcon test-result --test-result-base build/minimal_integration_test
echo $?
```
