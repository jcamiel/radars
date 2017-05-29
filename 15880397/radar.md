# Reachablity Sample Broken on 64-bit Architecture

Number: [rdar://15880397](http://openradar.appspot.com/15880397)    
Date Originated: 22-Jan-2014 03:45 PM  
Status: Closed  
Resolved: 
Product: iOS SDK  
Version: 7.0.4  
Classification: Serious bug  
Reproducible: Always  

## Summary:

On a 64-bit device (an iPhone 5s for instance), Reachability sample produces incorrect values for cellular availability when the sample is built with armv7 - armv7s - armv64 architectures.

Building the sample with only armv7 - armv7s produces the correct values for cellular data availability.


## Steps to Reproduce:

1. Download the Reachability sample from the developer library (<https://developer.apple.com/library/ios/samplecode/Reachability/Introduction/Intro.html#//apple_ref/doc/uid/DTS40007324>).
2. Build the sample with Xcode 5.0.2
3. Run it on an iPhone 5s with cellular connection available; the sample shows that: "Cellular data network is active. Internet traffic will be routed through it."
4. In the sample build settings, select "Standard architectures (including 64-bit) (armv7, armv7s, armv64)" (the default configuration is "Standard architectures (armv7, armv7s)")
5. Re-run the sample on an iPhone 5s with an active cellular connection: the sample doesn't show the availability of the cellular connection.

## Expected Results:

Reachability sample should show the availability of the cellular connection, even if the sample has been built with 64-bit architectures.

## Actual Results:

Reachability sample doesn't show the availability of the cellular connection.
