# UIAlertView dims controls issue on iOS 7 when dismissed in background.

Number: [rdar://15582862](http://openradar.appspot.com/15582862)    
Date Originated: 04/12/2013  
Status: Duplicate of 14924714 (Open)  
Resolved: 
Product: iOS  
Version: iOS 7.0.4  
Classification: UI/Usability  
Reproducible: Always  

## Summary:

When an UIAlertView is shown on iOS 7, all controls below the UIAlertView are greyed to emphasise the alert and re-colored on the UIAlertView dismisses. 

A best practice very often advertised by Apple with UIAlertView is to dismiss an UIAlertView when your app goes in background. 

Doing this, from iOS 4 to iOS 6 has been really simple and straightforward. 

Given a view controller that has a IBAction showing an UIAlertView:

    - (IBAction)tap:(id)sender
    {
        self.alertView = [[UIAlertView alloc] initWithTitle:@"Hello"
            message:@"A standard UIAlertView"
            delegate:nil
            cancelButtonTitle:@"OK"
            otherButtonTitles:nil];

        [self.alertView show];
    }

One has just register to UIApplicationDidEnterBackgroundNotification in viewDidLoad :

    - (void)viewDidLoad
    {
        [super viewDidLoad];

        [[NSNotificationCenter defaultCenter] addObserver:self
            selector:@selector(applicationDidEnterBackground:)
            name:UIApplicationDidEnterBackgroundNotification
                object:nil];

    }

and dismiss the UIAlertView when handling UIApplicationDidEnterBackgroundNotification:

    - (void)applicationDidEnterBackground:(NSNotification *)theNotification
    {
        NSInteger cancelButtonIndex = self.alertView.cancelButtonIndex;
        [self.alertView dismissWithClickedButtonIndex:cancelButtonIndex
                                             animated:NO];
    }

On iOS 7, this code should have work flawlessly. The alert view is dismissed when the app goes into background. But the app is activated again into foreground, all controls that have been automatically dimmed by the system while the alert view was shown are still dimmed.

## Steps to Reproduce:

1. Create a simple app with a view controller
2. Add a UIButton that show an UIAlertView.
3. In the viewDidLoad method of this UIViewController, register to UIApplicationDidEnterBackgroundNotification to dismiss a potential alert view.
4. In the handler of UIApplicationDidEnterBackgroundNotification, dismiss the UIAlertView
5. Launch the app, tap on the button to show an alert view.
6. While the alert view is shown, send the app to the background.
7. Launch the app, the alert view has been dismissed, but the dimmed controls are still gray and active.

## Expected Results:

The dimmed controls should have recovered their tintColor.

## Actual Results:

The dimmed controls are greyed.
