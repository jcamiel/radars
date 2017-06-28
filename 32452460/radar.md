# WKWebView Doesn't Take NSHTTPCookieStorage Session Cookies into Account

Number: [rdar://32452460](http://openradar.appspot.com/32452460)    
Date Originated: 29-May-2017 01:00 PM  
Status: Duplicate/17486250  
Resolved:  
Product: iOS + SDK WebKit
Version: iOS 10.3.2  
Classification: Other Bug  
Reproducible: Always  

## Summary:

NSHTTPCookieStorage manages storage of cookies. If an application creates a session cookie and adds it to the NSHTTPCookieStorage singleton, UIWebView sends this cookie, whereas WKWebView doesn't send it. The documentation of NSHTTPCookieStorage says that "As a rule, cookies are shared among all applications and are kept in sync across process boundaries. Session cookies (where the cookie object’s sessionOnly method returns YES) are local to a single process and are not shared.". But for the app developper, WKWebView can (and should) be used for drop-in replacement of UIWebView (since UIWebView is deprecated on iOS 9), regardless WKWebView is sandboxed compared to UIWebView. In particular, all session cookies positionned by an app should be honoured by WKWebView in the context of this particular application. As a side note, there are multiple use cases where session cookie are useful (limited login etc...) in an application.

## Steps to Reproduce:

1. Create an iOS application with one UIWebView and one WKWebView
2. Create a session cookie and a cookie with an expiration date in the app:

		- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

			[self addCookies];

			return YES;
		}


		- (void)addCookies {

			NSDictionary *properties1 = @{
				NSHTTPCookieName: @"cookie_session",
				NSHTTPCookieValue: @"value1",
				NSHTTPCookieDomain: @".kermit.orange-labs.fr",
				NSHTTPCookiePath: @"/",
			};
			NSHTTPCookie *cookie1 = [NSHTTPCookie cookieWithProperties:properties1];

			[[NSHTTPCookieStorage sharedHTTPCookieStorage] setCookie:cookie1];

			NSDate *nowPlus15Minute = [NSDate dateWithTimeIntervalSinceNow:15 * 60];
			NSDictionary *properties2 = @{
										  NSHTTPCookieName: @"cookie_with_expiration_date",
										  NSHTTPCookieValue: @"value2",
										  NSHTTPCookieDomain: @".kermit.orange-labs.fr",
										  NSHTTPCookiePath: @"/",
										  NSHTTPCookieExpires: nowPlus15Minute,
										  };
			NSHTTPCookie *cookie2 = [NSHTTPCookie cookieWithProperties:properties2];

			[[NSHTTPCookieStorage sharedHTTPCookieStorage] setCookie:cookie2];
		}


3. Load the url <http://cookie.kermit.orange-labs.fr> from the UIWebView and the WKWebView. Note: <http://cookie.kermit.orange-labs.fr> is a web page that display cookies set by the request, but test web page could be used. 

Alternative:

1. Build and run the provided sample.

## Expected Results:

UIWebView and WKWebView should display the two cookies 'cookie_session' and 'cookie_with_expiration_date'.

## Actual Results:

WKWebView only displays the 'cookie_with_expiration_date', whereas UIWebView displays both cookies.

## Version:

iOS 10.3.2 (14F89)

## Notes:

##Configuration:

Tested on iPhone SE iOS 10.3.2
