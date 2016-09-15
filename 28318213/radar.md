# QLPreviewController is leaking on iOS 10.

Number: [rdar://28318213](http://openradar.appspot.com/28318213)    
Date Originated:	15-Sep-2015 01:00 PM    
Status:    
Resolved:	
Product:	iOS   
Version:	10
Classification: Other Bug  
Reproducible: Always   

## Summary:

When using QLPreviewController to preview a document (like a PDF file), instances are still leaving in memory even if the view controller is not used any more.

## Steps to Reproduce:

1. Download [Apple DocInteraction sample](https://developer.apple.com/library/content/samplecode/DocInteraction/Introduction/Intro.html)
2. Compile it with Xcode 8 / iOS 10
3. Run
4. Tap the first link to push Text Document.txt
5. Tap the back button to pop the QLPreviewController
6. Use Xcode 8 objects browser and look for instance of QLPreviewController UIViewController. There is one leaving instance whereas the view controller have been oped and should not be present in the view hierarchy.


Alternatively:

3. Modify the sample and subclass QLPreviewController:

        @interface MYViewController : QLPreviewController
        @end
        
        @interface MYViewController ()
        
        @end
        
        @implementation MYViewController
        
        - (void)dealloc {
        
        }
        
        @end

4. Run
5. Put a breakpoint in MYViewController's dealloc 
6. Tap the first link to push Text Document.txt
7. Tap the back button to pop the QLPreviewController
8. Breakpoint in dealloc is not raised, the instance of MYViewController is leaking


## Expected Results:

Not QLPreviewController instance should remain in memory after the view controller have been popped.

## Actual Results:

QLPreviewController instances remain in memory after the view controller have been popped.

## Version:

iOS  10.0.1 (14A403)

## Notes:

## Configuration:

iPhone SE 32 Go

## Attachments:


