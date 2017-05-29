# Set a key bindings for 'Archive' in Xcode 4.3 crashes Xcode

Number: [rdar://10926699](http://openradar.appspot.com/10926699)    
Date Originated: 24-Feb-2012 05:51 PM  
Status: Closed  
Resolved:  
Product: Developper Tools     
Version: Xcode Version 4.3 (4E109)  
Classification: Crash/Hang/Data Loss    
Reproducible: Always  

## Summary:

Set a key binding for 'Archive' in Xcode 4.3 crashes the application. As there is no default keyboard shortcut for Archive, setting a keyboard shortcut should be possible and not crash the application.

## Steps to Reproduce:

1. Launch Xcode 4.3
2. Go to Preferences
3. Go to Key Bindings
4. Search for Archive
5. Set a key for Archive (Product menu): for example Command Option E (⌥⌘ E)
6. Click anywhere 
7. Xcode crashes

## Expected Results:

Keyboard shortcut should be assigned and Xcode shouldn't crash.

## Actual Results:

Xcode crashes.

## Regression:

## Notes:

##Configuration:

