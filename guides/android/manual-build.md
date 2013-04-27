# Manual Build of Pender
this document outlines how you would construct a Pender project, uncluding dependencies, 'by hand'. Not that this process is not recommended: use the provided platform build tools instead. You can use this document as a guide to what a platform build tools needs to do in order to construct a pender project.

## Requirements
* the Android SDK
* Android tools on your PATH
* 

## Sections
* Create a Pender Library Project
* Create a Pender Client Project

## Create a Pender Library Project
the Pender library project holds the main Pender implementation, which a client project references.

### 1. Obtain the Pender source code
using git:

    git clone https://github.com/lorinbeer/pender

###  2. Create an Android Library Project
using the android command line tool, create a library project

this will house the Pender Implementation

    android create lib-project --name Pender --target <targetid> --path <path> --package com.pender

Name the project Pender, and leave the package as com.pender. Provide the path you want the library probject contstructed in and provide the target id.

The rest of the instructions will assume you have created the project in path ./PenderAndroidLibrary

The target id is the version of android this project targets, type:

    android list targets

for a list of targets on your system

### 3. Copy Pender source code from the root of the repo to the root of the library project
    
    cp -r pender-android/src /path/to/your/pender/library/project/src

so if you made the pender library in PenderAndroidLibrary in the same directory as the git repo, the command would be:

    cp -r pender-android/src ./PenderAndroidLibrary/src

### 4. Download Rhino 

* [Bitbucket hosted](https://bitbucket.org/lorinbeer/pender/downloads/rhino1_7Rpre.jar)
 
* [Sourceforge hosted](https://sourceforge.net/projects/penderstaticlib/files/rhino1_7R5pre.jar)

put the rhino1_7R5pre.jar file downloaded in 4 in ./PenderAndroidLibrary/libs 

5. Build the Library
test that everything is referenced and installed correctly by test building the Pender library project
    
    ant debug
or
    ant release

## Create a Pender Client Project
a client project is a project that consumes (uses) Pender

### 1. Create a regular Android Project
using the android command line tool again, create a regular Android project
    android create project --target <targetid> --path <path> --package <package> --activity <activityid>

where: 
* "<targetid>" = latest android target
* "<path>" = path to project, should be same dir as the Library Project
* "<package>" = com.pender.example or whatever you want to call your example
* "<activityid>" = name of the main activity of the example, let's go with "PenderExample" without the quotes

### 2. update the example project so it references the library

    android update project --path <path> --library <libloc>

"<path>" is path to your project
"<libloc>" is path to your library

assuming you've made both in the same toplevel directory as the repo, the command would be:

android update project --path ./PenderExample --library ./PenderAndroidLibrary

for project called PenderExample

### 3. copy over the assets directory to the client project

    cp -r pender-android/assets ./PenderExample/assets

for project called PenderExample

### 4. Provide a min-sdk-version
in order to function properly, add a minimum sdk version specification to the AndroidManifest.xml

    <uses-sdk android:minSdkVersion="8" />

### 5. Call the Pender Library from the main activity class of the Pender Example project 
look in PenderExample/src and follow the directory tree down to the activity

open up the activity located in PenderExample/src/com/pender/example/exampleactivity.java

replace everything under the package statement with:

    import android.app.Activity;
    import android.os.Bundle;

    import com.pender.Pender;

    public class PenderActivity extends Activity
    {
        /** Called when the activity is first created. */
        @Override
        public void onCreate(Bundle savedInstanceState)
        {
            super.onCreate(savedInstanceState);
            mPender = new Pender(this);
            mPender.init();
        }

        private Pender mPender;    
    }

### 6. Build and Install

    ant debug

or

    ant release

and install on a device or simulator

    adb install bin/blah.apk

where blah.apk will be something like PenderExample-debug.apk


