 
Summary:
The Accessibility Identifier of a view is sometimes not readable in the Accessibility section of the Object Inspector of the View Hierarchy Debugger.

Steps to Reproduce:
1. In an iOS project, set the accessibilityIdentifier on some of your views to make it easier to find them when debugging.
2. Click the Debug View Hierarchy button to switch to the view debugger.
3. Click on a view that you know to have the accessibility identifier set.
4. Look at the Accessibility section of the Object Inspector to see the identifier.

Expected Results:
The Identifier row shows the value of the accessibility identifier.

Actual Results:
The Identifier row, seemingly randomly, will show one of three things:
1. The accessibility identifier, as expected.
2. The accessibility identifier, followed by a double quote (could be a single quote - this is from memory), like this. If my view’s identifier is searchStack, the Identifier row shows what’s between the arrows: → searchStack" ←
3. The Identifier row says “unable to read data” (screenshot attached, and at http://cl.ly/fcSm

Regression:
unknown

Notes:
The identifier is definitely set correctly, and if I query it in the debugger, it’s fine:

(lldb) po [0x79eee7b0 accessibilityIdentifier]
searchStack

I’m seeing this in a Swift project. Haven’t tested Obj-C. I’m not doing anything fancy to set the identifier - just doing someView.accessibilityIdentifier = "someLiteralString" in my Swift code (not using xibs/storyboards).
Comments