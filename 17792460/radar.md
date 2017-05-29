# QLPreviewController View is all White when Embedded and Presented Modally in a Navigation Controller (iOS 8 b4)

Number: [rdar://17792460](http://openradar.appspot.com/17792460)    
Date Originated:	24-Jul-2014 10:57 AM    
Status:	Open    
Resolved:	
Product: iOS   
Version: 8
Classification:   
Reproducible: Always   

## Summary:

QLPreviewController on iOS 8 beta 4 has display issue when embedded and presented modally in a navigation controller. The issue can be easily reproduce using Apple sample DocInteraction <https://developer.apple.com/library/prerelease/ios/samplecode/DocInteraction/Introduction/Intro.htm>
On the simulator QLPreviewController works fine; on an iPhone 5 / iOS 8 beta 4, the preview is white.

## Steps to Reproduce:

1. Download the Apple DocInteraction sample that uses QLPreviewController <https://developer.apple.com/library/prerelease/ios/samplecode/DocInteraction/Introduction/Intro.html>
2. Build it with Xcode 5.1.1 (5B1008), and install it on a real device in iOS 8 beta 4 (for instance, iPhone 5)
3. Run the sample on the device, tap on 'PDF document.pdf' to open the preview view controller, the PDF document is shown
4. In the file DITableViewController.m, instead of pushing the preview controller on the current navigation controller, present it modally:    

	Original code:    
		
		// for case 3 we use the QuickLook APIs directly to preview the document -
		QLPreviewController *previewController = [[QLPreviewController alloc] init];
		previewController.dataSource = self;
		previewController.delegate = self;

		// start previewing the document at the current section index
		previewController.currentPreviewItemIndex = indexPath.row;
		[[self navigationController] pushViewController:previewController animated:YES];

	Modified code:    
		
		// for case 3 we use the QuickLook APIs directly to preview the document -
		QLPreviewController *previewController = [[QLPreviewController alloc] init];
		previewController.dataSource = self;
		previewController.delegate = self;

		// start previewing the document at the current section index
		UINavigationController *previewNavigationController = [[UINavigationController alloc] initWithRootViewController:previewController];

		previewController.currentPreviewItemIndex = indexPath.row;
		[[self navigationController] presentViewController:previewNavigationController animated:YES completion:nil];

5. Run the sample on the same device, tap on 'PDF document.pdf' to open the preview view controller, a white screen is shown.


## Expected Results:

The PDF document should be displayed.

## Actual Results:

A white view is displayed.

## Version:

iOS 8.0 (12A4331d)

## Notes:

The QLPreviewController has issue with txt, jpg, pdf and html.

## Configuration:

iPhone 5 16Go using iOS 8 beta 4