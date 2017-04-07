# XCTest : Multiples Matches Found with Only One Button in UI

Number: [rdar://31498932](http://openradar.appspot.com/31498932)    
Date Originated:  07-Apr-2017 01:00 PM    
Resolved: 
Product:  Developper Tools   
Version:  Xcode 8.3 - iOS 10.3
Classification: Serious Bug  
Reproducible: Always   

## Summary:

Since Xcode 8.3, I've a strange XCTest behaviour that happens only on iOS 10.3 devices / simulator.

I create a simple app:

- a UITableViewController that create a static UITableView (in IB)
- I add one cell in this tableview that only contains a UIButon with accessibilityIdentifier equal to "button1".

If I launch an UI test and log the buttons element

    po XCUIApplication().buttons =>
    
    Find: Target Application 0x6000000bafa0
        Output: {
            Application 0x60000016ce40: {{0.0, 0.0}, {414.0, 736.0}}, label: 'TestXC'
        }
        ↪︎Find: Descendants matching type Button
            Output: {
                Button 0x60000016ccc0: traits: 8589934593, {{19.0, 71.0}, {46.0, 30.0}}, identifier: 'button1', label: 'Button'
            }

There is only one button seen by the XCTest framework as expected and I can tap this button with a subscript:
let button = XCUIApplication().buttons["button1"]
button.tap()

This usecase is working perfectly on iOS 10.3, 10.2, 10.0 and 9.x.

If in this cell, I add a UISwitch, the buttons query is now:

    po XCUIApplication().buttons =>
    
    Find: Target Application 0x6000002a1560
        Output: {
            Application 0x600000175600: {{0.0, 0.0}, {414.0, 736.0}}, label: 'TestXC'
        }
        ↪︎Find: Descendants matching type Button
            Output: {
                Button 0x6080001735c0: traits: 8589934593, {{19.0, 71.0}, {46.0, 30.0}}, identifier: 'button1', label: 'Button'
                Button 0x608000173a40: traits: 8589934593, {{19.0, 71.0}, {46.0, 30.0}}, identifier: 'button1', label: 'Button'
            }

There are now 2 buttons for the identifier 'button1' !
If I try to target the button, I've now an error "Multiple matches found for "button1" Button", whereas there is still only one button, and only one UI element with accessibility identifier equal to "button1"

## Steps to Reproduce:

1. Install Xcode 8.3
2. Create a simple app with a UITableViewController and a static UITableView with one cell (you can use the sample provided)
3. In this cell, add a UIButton with accessibilityIdentifier set to "button1" and one UISwitch element
4. Add a UI test to tap this button: create a testSample method with this code

    func testExample() {
        let button = XCUIApplication().buttons["button1"]
        button.tap()
    }

## Expected Results:

The button should be tapped and the test should succeed.

## Actual Results:

The test fails because "Multiple matches found for "button1" Button"

## Version:

Xcode Version 8.3 (8E162)

## Notes:


##Configuration:

This test case is working with Xcode 8.3 on 10.2/10.1/10.0/9.x simulator. It fails only with 10.3 devices/simulator.

