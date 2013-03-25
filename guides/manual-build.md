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


