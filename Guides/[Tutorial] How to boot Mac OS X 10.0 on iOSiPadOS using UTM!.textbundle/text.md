
[Tutorial] How to boot Mac OS X 10.0 on iOS/iPadOS using UTM!

[

Tutorial

](https://www.reddit.com/r/jailbreak/?f=flair_name%3A%22Tutorial%22)

Hey guys!

exDeveloper here, and I will "teach" you how to boot Mac OS X 10.0 on iOS/iPadOS using UTM.

I got help from Pixelomer while doing this, so shoutout to him!

Here we go.

Things you need:

Mac with Xcode installed
iPhone, iPad, iPod Touch (wat?) with iOS 11 or later
If you are on iOS 13.3.1, you need paid Apple Developer Account.
Steps:

Follow tutorial on this link:
https://www.youtube.com/watch?v=bltM3h6Kqx8
Quick googling should let you find Mac OS X 10.0 iso file easily.
Go to this link https://github.com/utmapp/UTM
Click Clone or download
Copy the link given on Github, and open Xcode
On Xcode welcome screen, click Clone an existing project
Paste the URL at the top of the window
Clone and save
Close Xcode
Open Terminal
Type cd and drag and drop the cloned UTM project into Terminal
press enter
Type this: git submodule update --init --recursive
Go to Safari and go to this link: https://github.com/utmapp/UTM/actions?query=workflow%3ABuild
Click the first one in the list
Download and extract: Sysroot-x86 and Sysroot-arm64
Copy the folders to UTM project directory
Open UTM.xcodeproj
Click UTM with little blue icon at the left side bar
Go to signing and Capabilities
Choose your Apple Development account and change Bundle ID
and look for UTMQemuSystem.m file in left sidebar of Xcode
put // before the following lines:
[self pushArgv:@"-vga"];
[self pushArgv:@"qxl"];
Connect your device into your computer
Run the app!
AirDrop disk image you created to your iDevice and save it on your iDevice
AirDrop .iso file to your iPhone and save it on your iPhone (I don't think this is necessary but still do it)
Go to UTM app on your iDevice and press + on top right corner
Give it a name
Change Architecture to PowerPC
Tap Setup Drives
Tap + on top right corner
Tap Path
Tap + on top right corner
Tap Import
Tap .iso file
Tap on the disk file that you just imported
Navigate back
Navigate back
Tap + on top right corner
Tap Path
Tap + on top right corner
Tap Import
Tap .img file
Tap on img file that got imported
Navigate back
Navigate back
Tap Save
Tap (i) on the VM that you just created
Go to Sound
Disable Sound
Navigate Back
Tap Done
Run VM!
Linked mentions
0
No backlinks found.
Unlinked mentions