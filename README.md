# regressionSuite
A Regression Test suite for smaccm.

1) First step is to get the Osate 2 sources. This regression suite will work with the bundled Osate 2, but the current usage and the following instructions assume you are running from source. Make sure you can get Osate 2 up and running and at a minimum get the Toy_Example and verify you can run AGREE on this.

See https://wiki.sei.cmu.edu/aadl/index.php/Getting_Osate_2_sources

2) Install the RCPTT plugin in the Eclipse Modeling Tools that you just downloaded up there in step 1. This can be found in the Eclipse Marketplace with a search for "rcptt". I have the current version 2.0.0 installed.

3) Now we need to increase the RCPTT timeout, this is very important for those models that will take a long time to run. In the Eclipse Preferences, click the "RCP Testing Tool" in the left pane. In the resulting page, change the "Launch timeout (sec):" from 300 to 600. Though not obvious by the field name, this will dictate how long individual test cases can run. The 600 seconds seems to be a big enough number but you're free to make this bigger.

4) Check out this regression suite to the Eclipse Modeling Tools Workspace that you have previously set up for running Osate 2. This is the workspace that will have folders like "osate2-ba", "osate2-core", ... "smaccm". 

5) Import the regressionSuite project in to your Eclipse Modeling Tools. The test suite project is in \regressionSuite\rcpttSuite.

6) To run the regression suite you will need to create a new Run Configuration in a similar fashion to the configuration you've already made to launch and run Osate 2.

Open the Run Configurations dialog, find the "Eclipse Application under Test" and right-click to create a new launch. In the new configuration click "Select..." button and choose "Osate 2 product". Click Apply, Run and off we go to Osate 2...

7) In the freshly launched Osate2 application we'll want to import the Toy_Example project from the smaccm checkout. This is likely located in the Eclipse Modeling Tools workspace (not in the Osate2 workspace). Click File->Import->Existing Projects and navigate to the Eclipse Modeling Tools workspace, you'll then find the model projects under "\smaccm\models\Toy_AGREE_Models". 

8) In the Eclipse Modeling application and switch to the RCPTT Perspective. Expand the regressionSuite project in the Test Explorer view. Further, expand the Toy_Example folder and observe the names of the objects within. Items starting with "tc_" are individual RCPTT test cases. The item starting with "ts_" is the Test Suite. To run an individual test case, double-click the desired item and in the newly opened view click the "Replay" button in the upper right. You will see activtiy begin in the Osate application as the test case runs. Upon completion you can see the results of the test case in the "Execution View".

The Test Suite will run all the test cases listed within. Double click the "ts_Toy_Example" to open the suite to see all the test cases. Clicking the "Execute" button in the upper right will run the test suite and again the results will be display in the "Execution View".

9) After this you may import other model projects from the smaccm repo in to Osate, and if there is a corresponding Test Suite in your Eclipse Modeling Test Explorer you may run these. 

10) At the top level of the regressionSuite in the Test Explorer you will see a "masterSuite". This is the top level test suite which will invoke all the individual test suites. Running this masterSuite does assume that you have imported all the corresponding models in to your Osate application.

----------------------------------------------------
# Anomalies

One semi frustrating "feature" is that the "Eclipse Application under Test" may hang when launched. This is the Run Configuration we made to launch Osate for RCPTT. This seems to occur when the Osate 2 launch does not exit cleanly. Unfortunately it isn't always obvious that this has happened if you aren't specifically watching for this event. What you'll notice is that Ostate 2 will probably launch and start, but in your Eclipse Modeling you will notice the Progress will be stuck at 57%. If you attempt to run a test case or test suite you will get a cryptic error in the RCPTT Execution View stating that "Connection is not Available". You'll also notice that your test cases don't run. The solution to this is to close Osate 2 and then close Eclipse Modeling. Relaunch Eclipse Modeling and open the Run Configurations, delete the "Eclipse Application Under Test" launch that we had previously created earlier in the instructions above. Then recreate the Eclipse AUT launch with the Osate 2 product Target. All should be well again after this...

----------------------------------------------------
# Under the Hood

The basis of all the test cases is in the following top level files:
   workbenchContext
   helperProcs
   testConfig
   userProcs
   
The workbenchContext is a RCPTT tool to configure the workbench state of the application under test, in our case Osate 2.

The testConfig.ctx file contains and handful of procedures, the two intended to be used in test cases are "test-setup" and "test-teardown". You should note that all the test cases are book-ended by these two procedure calls.

The userProcs.ctx contains the high level procedure calls that will generally be used to develop test cases. 

The helperProcs.ctx contains lower level procedure calls that in general are called from the high level userProcs.ctx procedures. These aren't typically called directly by test cases but these may be used directly for specific actions if needed.

