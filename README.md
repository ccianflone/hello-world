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
    * GraceNoteOptionsTest::thatGraceNoteOptionsProduceOptionalElements
    * GraceNoteOptionsTest::thatGraceNoteOptionsIsNotCreatedFromMarkupElementWithBogusElement
    * ...
    * BaselinesMarkupTest::thatMoveMappingSetterIsFoundForBaselinesSysLyricVerse
  * MMClefObjectTests
  * SpotlightMarkupTestCase

If you have introduced a failure, you may actually find it much easier to look in the Test Navigator and use the "Show only failing tests" icon that looks something like an x in a diamong at the bottom of the Test Navigator.  (Part of the reason this stopped working in Xcode is that we were not keeping up with latest versions of GTMGoogleTestRunner.mm.)

If you find you have broken an existing test you can now also right click on the test in the Test Navigator and select:

* Run "GraceNoteOptionsTest::thatGraceNoteOptionsProduceOptionalElements"

for example.  Also, clicking on a failed test will bring you to the source test where the failure occurred.  (Note: this does not currently work for passing tests.)  Note that you can also make an arbitrary selection of tests to run in the Test Navigator.

This time, let us assume you are using a TDD-work flow and want to quickly run tests in a given test suite, for example, GraceNoteOptionsTest.  You could of course simply do a full test run and wait the long time (currently abbout 60-100 seconds) for the tests to be generated in the Test Navigator.  Of course, everytime you add a new test you will have to do this.  Xcode does not automagically pick up the addition of these dynamically created tests the way it does with normal XCTestCase subclasses (which show up upon first compilation).  Instead, make use of an environment variable (GTEST_FILTER=GraceNoteOptionsTest*) to limit tests to just those tests.  You still need to do a full run of tests (Command-U) for those tests to show up in the Test Navigator but that process should be MUCH faster now.  You can then run just a selection of those tests in the Test Navigator as before.  Happy TDD-ing!

Finally, value paramtereized test now work on the Mac (along with potentially other options, including the use of command line arguments which are now passed correctly to google test).



