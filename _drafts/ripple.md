---
title: My first hackathon experience
layout: default
permalink: ripple
---

_12 hours of hacking and building the essentials_

![](/images/ripple/ripple-full.png)

I've been to the [AngelHack Hong Kong][1] last weekend. This is my first
time attending a real hackathon after an equally fantastic event [StartLab][2]
back in June.

I wasn't really preparing anything beforehead, but I got teamed up with
four other guys at the opening ceremony.

We came out with a location based chatting application called Ripple,
and our UI/UX Designer, Meng To, later wrote about [how we came up and proceed
with this idea][6].

![The concept](https://d233eq3e3p3cv0.cloudfront.net/max/994/0*NCAjrogmLTbredgU.png)

> _Meng described the design concept with a well created [Flinto
> prototype][Flinto]._

The prototype with static screens could pretty much representing our idea,
but there were two screens that we couldn't really demonstrate without a
working example.

### Part 1 - Signup screen with the live Camera

![Signup](/images/ripple/signup.gif)

> _`UITextField x 1`, `GPUImageView x 2` `UIButton x 1`_


The technical barriers of this screen contains two main features:

- Display the live camera in partial of the view
- Blur the live picture and blend it to the background

I started with a _Single View Based_ application, which I liked how Xcode
provides a minimum template with a `Main.Storyboard` properly set up,
and started implementing the video layer. 

I had already heard about the [BradLarson/GPUImage][3] few years ago,
it went viral since iOS 4 when Apple introducted the [AVFoundation][]
framework. 

The framework is on [Cocoapods][], it was a real quick one line configuration.

    pod 'GPUImage'

This was the first time I actually use GPUImage, the sample code contains
quite a number of sub projects and live camera filters. It took me some
time to understand it and it turned out that initializing a camera and
display on screen was pretty easy.

```objective-c
- (void)viewDidLoad {
    [super viewDidLoad];

    self.videoCamera = [[GPUImageVideoCamera alloc] initWithSessionPreset:AVCaptureSessionPreset640x480 cameraPosition:AVCaptureDevicePositionFront];
    self.videoCamera.outputImageOrientation = UIInterfaceOrientationPortrait;

    // self.avatarView is a non full screen GPUImageView instance
    // created in Storyboard
    [self.videoCamera addTarget:self.avatarView];
    [self.videoCamera startCameraCapture];
}
```

#### The blurry live background

My initial thought was to manually capture and create an image out of the `self.avatarView`, then do the blurring operation and assign it back to the background.

I quickly realized executing this way would probably turn the code into an ugly, slow,
complicated beast.

I double checked the GPUImage filter gallery and found the `GPUImageGaussianBlurFilter`.
Yes, we could directly process the live picture with the GPU, we just need to properly
setup the our view with the filtered output.

I added a full screen `GPUImageView`, and did some proper setup in code:

```objective-c
self.blurFilter = ({
    GPUImageGaussianBlurFilter *blurFilter = [[GPUImageGaussianBlurFilter alloc] init];
    blurFilter.blurSize = 8;
    blurFilter;
});

self.videoCamera addTarget:self.blurFilter];

// self.blurView is a fullscreen GPUImageView instance configured in Storyboard
[self.blurFilter addTarget:self.blurView];
```

Boom! No performance issue, clean code, happy engineer! :)

To add an extra touch, we masked the avatar into a perfect circle, thanks to the
research by our teammate, it was just a single line of code.

```objective-c
self.avatarView.layer.cornerRadius = self.avatarView.frame.size.width/2;
```

### Part 2 - Chat screen and the springy message bubbles

![Message bubbles](/images/ripple/message.gif)

> _Springy message bubbles are very fun to play with._

The next one we wanted to create the chat room view, like what we needed
to have to provide the best chatting experience.

We loved the iMessage style floating bubbles very much. Since WWDC 2013 we were told that 
the physics were done in a framework called UIKit Dynamics, and would be available to developers
through iOS 7 SDK.

It could easily took up few hours for learning the [sample code][7]. At the end
of the day, it was a hackathon. I googled for sample code and libraries, quickly
came across [tristanhimmelman / THSpringyCollectionView], got it smoothly compiled 
and ran on the simulator:

![Springy](/images/ripple/THSpringyCollectionView.png)

> _The runtime results with a block of yellow rectangles_

Twe needed no further investigation. The README containing keywords like
`UICollectionViewFlowLayout` and `UIAttachmentBehaviours` indicated that
it was the correct way of implementation.

I asked our designer to exported the message bubbles together with sample text.
With previous experience of working with UICollectionView, declaring an array
for the UICollectionViewDataSource was fairly straightforward.

#### The sliding keyboard

![Sliding Keyboard](/images/ripple/sliding-keyboard.gif)

> _When you drag your finger from the top way down to the bottom, the
keyboard also follows your touch and slides down._

The sliding keyboard was also first introduced by iMessage from Apple.
Facebook took this feature with their implemention on [chat heads][] for
their iOS app. I couldn't think of a reason for us not to do that on our
app.

Daniel Amitay has a fairly popular opensource project called [DAKeyboardControl][5]
quickly did the job, a warm reminder would be make sure you were required to
manually taking care of the [retain cycles][7], and also remove the observer
properly in dealloc.

```objective-c
- (void)viewDidLoad {
    [super viewDidLoad];

    
    __weak typeof (self) weakSelf = self;
    [self.view addKeyboardPanningWithActionHandler:^(CGRect
keyboardFrameInView) {
      // Becareful of the retain cycle and use weakSelf instead of self
      // when you need to add custom logic in code.
      CGRect tableViewFrame = weakSelf.messageView.frame;
      tableViewFrame.size.height = toolBarFrame.origin.y;
      weakSelf.messageView.frame = tableViewFrame;
    }];
}

- (void)dealloc {
    [self.view removeKeyboardControl];
}
```

## Conclusion

It is not necessary for us to implement all the screens and we were able
to save some time for a good sleep by skipping the entire backend.

We were very lucky to be able to build an MVP demonstrating our idea and
highlight our thoughts and attention to UX and details, that won us to the final
top three teams.

I'm very happy to be part of the hackathon and the team, we'll continue
on developing Ripple and we'll see how it goes!

_Special thanks to [Greg Gopman][], [Joshua Slayton][], and [Cassy Lau][] for hosting, 
sponsoring, and giving advise for Angelhack attendees. And also to my teammate Christopher,
Benny, Vincent, and last but not least, [Meng To][Meng] whom let me to use the cover image and
all the support on this blog post!_

[1]:https://apphack13hongkong.eventbrite.hk/
[2]:http://startlab.hk/
[3]:https://github.com/BradLarson/GPUImage 
[4]:https://medium.com/design-ux/bb582274b93f#0909-65cc77fc6194
[5]:https://github.com/danielamitay/DAKeyboardControl
[6]:https://medium.com/design-ux/bb582274b93f
[7]:https://developer.apple.com/library/IOS/samplecode/DynamicsCatalog/Introduction/Intro.html
[AVFoundation]:https://developer.apple.com/av-foundation/
[Meng]:http://mengto.com
[Cocoapods]:http://cocoapods.org
[tristanhimmelman / THSpringyCollectionView]:https://github.com/tristanhimmelman/THSpringyCollectionView
[chat heads]:https://www.facebook.com/help/101495056700254
[Flinto]:https://www.flinto.com/p/726e28f6
[Greg Gopman]:https://twitter.com/Gopmania
[Joshua Slayton]:https://angel.co/joshuaxls
[Cassy Lau]:https://angel.co/caseylau

