# Launching UIAutomation tests in CLI always open iPad Simulator for Universal app

Number: [rdar://13607967](http://openradar.appspot.com/13607967)    
Date Originated: 2013-04-09  
Status: Closed  
Resolved: 
Product: Developer Tools  
Version: Xcode 4.6.1  
Classification: Features  
Reproducible: Always     

## Summary:

When launching UIAutomation tests in command line, the iPad simulator is always opened for Universal app, and  there is also no simple way to set the Simulator device type. One possible way is to force TARGETED_DEVICE_FAMILY at build time to force the Simulator to either be iPhone or iPad. But in this case, we can also not tell the Simulator to be 3.5" or 4", or Retina and Not retina for instance.

## Steps to Reproduce:

1. Create a xcodeprojet for an Universal app in Xcode 4.6.1.
2. Create some UIAutomation script for this project:

        Test1.js:
        var testName = "Test 1";
        var target = UIATarget.localTarget();
        var app = target.frontMostApp();
        var window = app.mainWindow();

        UIALogger.logStart( testName );
        app.logElementTree();
        UIALogger.logStop( testName );

3. Launch instruments in command line for this script

        instruments \
        -t "/Applications/Xcode.app/Contents/Applications/Instruments.app/Contents/PlugIns/AutomationInstrument.bundle/Contents/Resources/Automation.tracetemplate" \
        name_of_app \
        -e UIASCRIPT absolute_path_to_the_test_file  

4. The iPad Retina Simulator is launching

## Expected Results:

There should be a way to precise which Simulator is launching at CLI for instruments.
Ideally, one could ask for "iPhone", "IPhone Retina 3.5", "iPhone Retina 4", "iPad", "iPad Retina", etc... 

## Actual Results:

There is no simple way to set the Simulator device type when launched in CLI.

## Notes:

