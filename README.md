# regressionSuite
A Regression Test suite for smaccm.

1) First step is to get the Osate 2 sources. This regression suite will work with the bundled Osate 2, but the current usage and the following instructions assume you are running from source. Make sure you can get Osate 2 up and running and at a minimum get the Toy_Example and verify you can run AGREE on this.

See https://wiki.sei.cmu.edu/aadl/index.php/Getting_Osate_2_sources

2) Install the RCPTT plugin in the Eclipse Modeling Tools that you just downloaded up there in step 1. This can be found in the Eclipse Marketplace with a search for "rcptt". I have the current version 2.0.0 installed.

3) Check out this regression suite to the Eclipse Modeling Tools Workspace that you have previously set up for running Osate 2.

4) Import the regressionSuite project in to your Eclipse Modeling Tools. The test suite project is in \regressionSuite\rcpttSuite.
You'll probably also notice that there is a \regressionSuite\testModel folder and project. Don't worry about this right now, this will be imported in to the Osate 2 workspace later.

5) To run the regression suite you will need to create a new Run Configuration in a similar fashion to the configuration you've already made to launch and run Osate 2.

Open the Run Configurations dialog, find the "Eclipse Application under Test" and right-click to create a new launch. In the new configuration click "Select..." button and choose "Osate 2 product". Click Apply, Run and off we go to Osate 2...

