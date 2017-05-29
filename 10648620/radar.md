# Xcode 4.2.1: UIAutomation setPreferencesValueForKey not mapped to NSUserDefault

Number: [rdar://10648620](http://openradar.appspot.com/10648620)    
Date Originated:  05-Jan-2012 06:49 PM    
Status: Closed  
Resolved:  
Product:  Developper Tools   
Version:  Xcode  
Classification: Serious  
Reproducible: Always   

## Summary:

In UIAutomation script, one can set setPreferencesValueForKey on UIATarget.localTarget.frontMostApp to change the preferences of an app. Doing this doesn't produce result while inspecing NSUserDefaults in the app.

## Steps to Reproduce:

1. write a UIAutomation test script
2. In the script, do the following 
        
        UIATarget.localTarget().frontMostApp().setPreferencesValueForKey("aValue", "someKey");

3. In the app, log the following
    
        NSUserDefaults *userDefaults = [NSUserDefaults standardUserDefaults] ;
        NSString *aValue = [userDefaults objectForKey:@"someKey"];
        NSLog("aValue=%@", aValue);

## Expected Results:

The UIAutomation should set the preferences object of NSUserDefaults

## Actual Results:

The UIAutomation doesn't set the preferences object of NSUserDefaults

## Notes:

On the iOS Simulator, preferences of an app are stored in ~/Library/Application Support/iPhone Simulator/5.0/Applications/xxxxxxxxx/Library/Preferences/com.mycompany.monapp.plist

The UIAutomation seems to stored the result in 
~/Library/Application Support/iPhone Simulator/5.0/Library/Preferences/com.mycompany.monapp.plist

