# UIImageView rendering issue with some particular PNGs.

Number: [rdar://17794018](http://openradar.appspot.com/17794018)    
Date Originated: 24-Jul-2014 03:32 PM    
Status:	Duplicate of 16603505 (Open/Closed)    
Resolved:	
Product: iOS   
Version: 8
Classification: Bug  
Reproducible: Always   

## Summary:

UIImageView shows rendering issues with some PNGs when app is run on device, on iOS 8 beta 4. For instance, the file [GrayLine@2x.png][] (produced with Photoshop) attached is rendered as a uniform gray rectangle on iOS 7 and shows a black buggy artefact on iOS 8 beta 4 using a real device (iPhone 5 for instance).
The image provided is a 2px by 198px uniform gray PNG (color used is 0xF7F7F7).
When changing the size of this PNG to 198px by 198px, the rendering is good.
When keeping the size and using another color (0xf7bf11 for instance) the rendering is good.

## Steps to Reproduce:

1. Create a simple iOS app using Xcode 5.1.1: a view controller with one view 
2. Create programatically an UIImageView of 200pt by 200pt and add it to the view controller's view
3. Set the image of the image view to the image provided [GrayLine@2x.png][] 
4. Build and run the app on a real device (iPhone 5C), with iOS 8 beta 4

Alternately, one can use the provided sample.

## Expected Results:

The view should display a uniform gray rectangle

## Actual Results:

The view displays a gray rectangle with a black bottom border

## Version:
iOS 8.0 (12A4331d)

## Notes:

## Configuration:

iPhone 5 16Go iO8 beta 4.

## Attachments:

[GrayLine@2x.png][]    
[SampleLine.zip][]    
[iOS7.png][]    
[iOS8.png][]    

[GrayLine@2x.png]: https://raw.githubusercontent.com/manbolo/radars/master/17794018/GrayLine@2x.png
[SampleLine.zip]: https://raw.githubusercontent.com/manbolo/radars/master/17794018/SampleLine.zip
[iOS7.png]: https://raw.githubusercontent.com/manbolo/radars/master/17794018/iOS7.png
[iOS8.png]: https://raw.githubusercontent.com/manbolo/radars/master/17794018/iOS8.png
