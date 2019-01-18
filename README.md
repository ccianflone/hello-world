# MakeMusic ReadMe

Here is a second version of README.md file.  Does it supersede a plain old "README" file with no extension?
Going to try a quick stab at docu for googletest and integration with XCTest in Xcode

GTMGoogleTesRunner.mm is a file that appears to have been copied from https://github.com/google/google-toolbox-for-mac/blob/master/UnitTesting/GTMGoogleTestRunner.mm

In particular, this attempts to integrate Google tests with the Xcode/XCTest infrastructure in Xcode.  At the time of this writing, recents changes to this file have improved support for this integration in Xcode 9.4.x and Xcode 10.x on both macOS 10.13.x and macOS 10.14.x systems.

We will cover some of the additions
