# MakeMusic ReadMe

Here is a second version of README.md file.  Does it supersede a plain old "README" file with no extension?
Going to try a quick stab at docu for googletest and integration with XCTest in Xcode

GTMGoogleTesRunner.mm is a file that appears to have been copied from https://github.com/google/google-toolbox-for-mac/blob/master/UnitTesting/GTMGoogleTestRunner.mm

This file attempts to provide integratation of Google tests with the Xcode/XCTest infrastructure in Xcode.  At the time of this writing, recents changes to this file have improved support for this integration in Xcode 9.4.x and Xcode 10.x on both macOS 10.13.x and macOS 10.14.x systems.

We will cover some of the additions to this source by covering a few common workflows in MakeMusic development.

Let's say you have just finished work on some feature or defect in Finale.  You added unit tests, correct?  Well, maybe you didn't add any google tests this time around and relied on our CppUnitLite testing or Finale Automation UI testing.  It would still be a good idea to run ALL the google tests before committing.  This can be done in Xcode by selecting Product > Test (Command-U).  You can see all the tests running by watching the console in Xcode OR NOW you can switch to the Test Navigator or Report Navigator to see which tests passed and which failed.  Previously you would seen a Test Navigator that looked like this:

* FinaleXCTests
  * FinCocoaPrintTests
  * GTMGoogleTestRunner
    * NO TESTS LISTED HERE
  * MMClefObjectTests
  * SpotlightMarkupTestCase

But now you will see something more like this:

* FinaleXCTests
  * FinCocoaPrintTests
  * GTMGoogleTestRunner
    * GraceNote first test
    * ...
    * ending test
  * MMClefObjectTests
  * SpotlightMarkupTestCase

If you have introduced a failure, you may actually find it much easier to look in the Test Navigator and use the "Show only failing tests" icon that looks something like an x in a diamong at the bottom of the Test Navigator.  (Part of the reason this stopped working in Xcode is that we were not keeping up with latest versions of GTMGoogleTestRunner.mm.)



