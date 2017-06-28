# XCTest Randomly Hangs iOS Simulator

Number: [rdar://xxx](http://openradar.appspot.com/xxx)    
Date Originated: 28-Jun-2017 01:00 PM
Status: Open
Resolved: 
Product:  Developer Tools
Version: Xcode 8.3.2 (8E2002)
Classification: Crash/Hang/Data Loss
Reproducible: Sometimes  

## Summary:

When launching XCTest for an iOS project from a Mac mini (Late 2012), XCTest randomly hangs with the followings logs :

2017-06-27 16:30:47.545 xcodebuild[87277:2923823] Error Domain=IDETestOperationsObserverErrorDomain Code=13 "Failed to background test runner. If you believe this error represents a bug, please attach the log file at /var/folders/cq/7r2qyr3x6yzfchvxgv2d8ghw0000gn/T/tmp.3QnBG6gL/Logs/Test/9BDF8038-25BF-4ACD-8ED1-6C33E072C6DC/Session-TestsUIOrangeEtMoi-2017-06-27_162653-unknWn.log" UserInfo={NSLocalizedDescription=Failed to background test runner. If you believe this error represents a bug, please attach the log file at /var/folders/cq/7r2qyr3x6yzfchvxgv2d8ghw0000gn/T/tmp.3QnBG6gL/Logs/Test/9BDF8038-25BF-4ACD-8ED1-6C33E072C6DC/Session-TestsUIOrangeEtMoi-2017-06-27_162653-unknWn.log}

Testing failed:
    Test target TestsUIOrangeEtMoi encountered an error (Failed to background test runner. If you believe this error represents a bug, please attach the log file at /var/folders/cq/7r2qyr3x6yzfchvxgv2d8ghw0000gn/T/tmp.3QnBG6gL/Logs/Test/9BDF8038-25BF-4ACD-8ED1-6C33E072C6DC/Session-TestsUIOrangeEtMoi-2017-06-27_162653-unknWn.log)
** TEST FAILED **

2017-06-27 16:29:46.889 XCTRunner[92374:2934762] Running tests...

Unexpected failure with no current test or suite:
    Failed to receive completion for <XCDeviceEvent:0x79840760 page 12 usage 64 duration 0.01s within 30.0s

Log file have been attached.

## Steps to Reproduce:

1. Build an iOS project
2. Run the tests for the iOS simulator on a low end machine from the command line:

    xcodebuild \
        -project "${PROJECT}" \
        -scheme ${TARGET} \
        -destination "${PLATFORM}" \
        test
3. Loop the test and wait for failure


## Expected Results:

XCTest should not hang.

## Actual Results:

XCTest is hanging.

## Version:

Xcode 8.3.2 (8E2002) / macOS Sierra 10.12.5

## Notes:

The hang seems to be reproductible on low end machines (see configuration.)

## Configuration:

Mac mini (Late 2012)
Processor 2.5 GHz Intel Core i5
Memory 8 BG 1600 MHz DDR3
Startup Disk SSD
Graphics Intel HD Graphics 4000 1536 MB


