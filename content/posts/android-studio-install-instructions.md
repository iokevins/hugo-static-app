---
title: 'Android Studio 1.5 Install Instructions: Debian Stretch (Testing)'
date: 2015-11-21T07:18:00.000-08:00
draft: false
tags: 
- jre
- android studio
- stretch
- jdk
- linux
- debian
- oracle
- android
- openjdk
- java
---

### Preparations - Packages and Environment

*   Java Development Kit (JDK)

*   Implements the Java Platform, Standard Edition (Java SE)
*   Two main versions:

1.  Oracle Corporation's [Java Development Kit](https://en.wikipedia.org/wiki/Java_Development_Kit) (JDK)
2.  [OpenJDK (Open Java Development Kit)](https://en.wikipedia.org/wiki/OpenJDK), "a free and open source implementation of the [Java Platform, Standard Edition (Java SE)](https://en.wikipedia.org/wiki/Java_Platform,_Standard_Edition)"

*   OpenJDK 7 versus Oracle JDK 7 

*   Google staff officially recommend Oracle JDK 7, on Linux ([via](https://developer.android.com/sdk/index.html#Requirements))
*   OpenJDK 6 was [engineered as a retrofit, from JDK 7, to JDK 6](https://community.oracle.com/blogs/robogeek/2009/01/05/it-will-be-openjdk7-where-openjdkjdk), which may have contributed to the current Google recommendation, in favor of Oracle JDK
*   However, OpenJDK 7 has a number of points in its favor:

*   Since 1.7, performance seems equivalent between OpenJDK and OracleJDK
*   Android itself builds from OpenJDK ([via](http://askubuntu.com/a/643782))
*   OpenJDK represents the official reference implementation of Java SE, since version 7 ([via](https://en.wikipedia.org/wiki/OpenJDK))

*   Winner: OpenJDK

*   [OpenJDK](http://openjdk.java.net/install/)

*   Debian Stretch (Testing) comes with the OpenJDK Java Runtime Environment (JRE), only (package openjdk-7-jre)
*   sudo apt-get install openjdk-7-jdk default-jdk
*   Note: default-jdk and openjdk-7 currently seem  the same, at the time of this writing
*   Environment variables configuration, via appending the following lines to ~/.bashrc:

*   vim ~/.bashrc
*   export JAVA\_HOME=/usr/lib/jvm/default-java
*   export PATH=$PATH:$JAVA\_HOME/bin

*   [Oracle Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/index.html) - Optional; Recommended, by Google staff

*   [Overview](http://ridz1ba.blogspot.com/2015/07/how-to-install-oracle-java-and-android.html)
*   Download the JDK

*   Navigate to [Oracle Java SE Downloads](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
*   At the top of the screen, select icon over text "Java Platform (JDK) 8u65 / 8u66" (alternatively, under section "Java Platform, Standard Edition", near text "JDK", select button "Download")
*   On screen "Java SE Development Kit 8 Downloads":

*   Under section "Java SE Development Kit 8u66"
    *   Select "Accept License Agreement" radio button
    *   Product / File Description: Linux x64
    *   Select file link (for example, jdk-8u66-linux-x64.tar.gz)

*   Under section "Java SE Development Kit 8u66 Demos and Samples Downloads"

*   Select "Accept License Agreement" radio button
*   Product / File Description: Linux x64
*   Select file link (for example, jdk-8u66-linux-x64-demos.tar.gz)

*   Navigate to [Oracle Java SE download page](http://www.oracle.com/technetwork/java/javase/downloads/index.html)

*   Under section "Additional Resources", row "Java SE 8 Documentation", select button "Download"
*   On screen "Java SE Development Kit 8 Documentation", scroll down to section "Java SE Development Kit 8u66 Documentation":
    *   Select "Accept License Agreement" radio button
    *   Product / File Description: Documentation 
    *   Select file link (for example, jdk-8u66-docs-all.zip)

*   Alternatively, [purge OpenJDK](http://www.2daygeek.com/uninstall-oracle-java-openjdk-linux/) (?)
*   Install the JDK
*   Note: abandoning this effort; staying with OpenJDK

*   [VM Acceleration](https://developer.android.com/tools/devices/emulator.html#vm-linux) (optional):

*   sudo apt-get install qemu-kvm libvirt-bin virtinst
*   Via: [KVM (Debian Wiki)](https://wiki.debian.org/KVM)
*   sudo adduser k kvm
*   sudo adduser k libvirt
*   Reboot
*   Enter BIOS setup utility

*   BIOS version: 1.39 (6QET69WW)
*   Config > CPU
*   Intel (R) Hyper-Threading Technology: Enabled

*   Note: "Enabled: This setting enables additional CPU threads. These threads appear as additional processors but share some resources with other threads within a CPU."
*   Note: "Disabled: This setting enables only one thread within each execution core unit."

*   Intel (R) Virtualization Technology: Enabled

*   Note: "When enabled, a VMM can utilize the additional hardware capabilities provided by Intel (R) Virtualization Technology"

*   Intel (R) VT-d Feature: Enabled

*   Note: "Intel (R) VT-d is Intel (R) Virtualization Technology for Directed I/O"

*   Save and Reboot

*   Other (important!)

*   sudo apt-get install lib32z1 lib32ncurses5 lib32stdc++6
*   [Via](https://stackoverflow.com/questions/28847151/unable-to-install-android-studio-in-ubuntu)
*   Note: lib32bz2-1.0 suggested but not found; doesn't seem needed (?) 

### Install folder considerations, on Debian:

*   Debian [filesystem overview](https://wiki.debian.org/FilesystemHierarchyStandard):

*   System-wide: /opt, "can be used to store addition software for your system, which is not handled by the package manager."
*   User-specific: /usr/local , "contains the majority of user utilities and applications, and partly replicates the root directory structure, containing for instance, among others, /usr/bin/ and /usr/lib."

*   Storage space: 

*   Does the folder's mount point have enough storage? 
*   For example, "/" and "/home" may lie in separate 

*   Note: 

*   I initially attempted an install to /opt
*   This succeeded, save for running out of storage, during download of components

### Installation Notes

*   Download Android Studio, for Linux

*   Using a web browser, navigate to [https://developer.android.com/sdk/index.html](https://developer.android.com/sdk/index.html)
*   Following instructions on the web site, download the current version (namely, as of this writing: android-studio-ide-141.2422023-linux.zip)
*   Note: Google seems to offer a bundled download--IDE and the SDK--but only for the Microsoft Windows version

*   Environment variables, to simplify subsequent commands:

*   export ASROOT=~/Android/
*   export ASZIP=~/Downloads/android-studio-ide-141.2422023-linux.zip

*   Create the install folder:

*   mkdir "$ASROOT"
*   Note: if exists, will fail, with error "mkdir: cannot create directory ‘/home/k/Android/’: File exists"

*   Unzip the downloaded file:

*   unzip "$ASZIP" -d "$ASROOT"

*   Permissions update (optional step, if system-wide install folder, such as /opt)

*   sudo chown k:k -R "$ASROOT/android-studio"
*   sudo mkdir -p "$ASROOT/android-sdk"
*   sudo chown k:k -R "$ASROOT/android-sdk"
*   Note: "If you install to /opt, you'll need to fix permissions vis chown to a suitable user" ([via](http://wiki.ros.org/android/Android%20Studio/Download))

*   [via](http://techgeek4shfl.blogspot.com/2015/08/install-android-studio-on-gnulinux.html); modified

*   Install Android Studio for Linux

*   "$ASROOT/android-studio/bin/studio.sh"
*   Loading screen:

*   Ignore terminal window warning "WARN - dea.updater.SdkComponentSource - Couldn't find existing SDK"

*   Screen "Complete Installation":

*   Select radio button "I do not have a previous version of Studio or I do not want to import my settings", then select button "OK"
*   Note: this represents an initial install; your mileage may vary...choose an appropriate option

*   Screen "Welcome": 

*   Ignore warning "System Health - OpenJDK shows intermittent performance and UI issues. We recommend using the Oracle JRE/JDK. Do not show again."
*   Select button "Next"

*   Screen "Install Type":

*   Select radio button "Custom"
*   Select button "Next"

*   Screen "Select UI Theme":

*   Select default option "IntelliJ"
*   Select button "Next"

*   Screen "SDK Components Setup":

*   Check the following checkboxes:

*   Android SDK -- (265 MB)
*   Android SDK Platform

*   API 23: Android 6.0 (Marshmallow) -- (67.1 MB)

*   Android Virtual Device -- (1 GB)

*   Android SDK Location:

*   We're accepting the default, for this guide
*   Optionally, specify an alternative location
*   For example, /opt/android-sdk

*   Select button "Next"

*   Screen "Verify Settings":

*   Accept defauts
*   Select button "Next"

*   Screen "Emulator Settings":

*   Accept defaults
*   Select button "Finish"

*   Screen "Downloading Components":

*   Watch the downloader complete various steps:

*   Downloading android-sdk\_r22.6.2-linux.tgz from https://dl.google.com/android/android-sdk\_r22.6.2-linux.tgz
*   Unpacking android-sdk\_r22.6.2-linux.tgz
*   tar xzvfC /tmp/AndroidStudio1FirstRun/android-sdk\_r22.6.2-linux.tgz /tmp/AndroidStudio1FirstRun/android-sdk\_r22.6.2-linux.tgz-unpacked
*   Installing Archives:
*     Preparing to install archives
*     Installing Google APIs, Android API 23, revision 1
*       Installed Google APIs, Android API 23, revision 1
*     Installing SDK Platform Android 6.0, API 23, revision 1
*       Installed SDK Platform Android 6.0, API 23, revision 1
*     Installing Android SDK Build-tools, revision 23.0.2
*       Installed Android SDK Build-tools, revision 23.0.2
*     Installing Android Support Repository, revision 25
*       Installed Android Support Repository, revision 25
*     Installing Google Repository, revision 23
*       Installed Google Repository, revision 23
*     Installing Android SDK Platform-tools, revision 23.0.1
*     Stopping ADB server failed (code -1).
*       Installed Android SDK Platform-tools, revision 23.0.1
*     Installing Sources for Android SDK, API 23, revision 1
*       Installed Sources for Android SDK, API 23, revision 1
*     Installing Google APIs Intel x86 Atom System Image, Google Inc. API 23, revision 9
*       Installed Google APIs Intel x86 Atom System Image, Google Inc. API 23, revision 9
*     Installing Android SDK Tools, revision 24.4.1
*       Installed Android SDK Tools, revision 24.4.1
*       Updated ADB to support the USB devices declared in the SDK add-ons.
*       Stopping ADB server succeeded.
*       Starting ADB server succeeded.
*     Done. 9 packages installed.
*   Android SDK is up to date.
*   Creating Android virtual device
*   Android virtual device Nexus\_5\_API\_23\_x86 was successfully created

*   When finished, select button "Finish"

*   Screen "Welcome to Android Studio"

*   Select link "Check for updates now", at the bottom of the screen
*   Handle appropriately

*   Errors and warnings:

*   Terminal messages:

*   (java:4035): GLib-GObject-WARNING \*\*: /build/glib2.0-ocmJ1Y/glib2.0-2.46.2/./gobject/gsignal.c:3484: signal name 'selection\_changed' is invalid for instance '0x7f2e0010a720' of type 'JawImpl\_2058'

*   Ignore
*   Seems like a minor known issue

*   Installer messages:

*   Fatal error, "Unable to run mksdcard SDK tool." (note: solved by installing lib32stdc++6, above)
*   Read timed out

*   Retry
*     
    

*   Fatal error, "platform-tools, tools and 5 more SDK components were not installed" (note: "Download interrupted: Read timed out", most likely caused by coffee shop wifi service interruption)

*   Create Debian "Activities" menu icon

*   Activities > "Main Menu"
*   Applications > Programming
*   Select button "New Item"

*   Name: Android Studio
*   Command: ~/Android/android-studio/bin/studio.sh
*   Comment: Google's Programming IDE for Android
*   Select the icon image, then choose file: ~/Android/android-studio/bin/studio.ico
*   Select button "OK"

*   Select button "Close"
*   Launch the new icon and add it to Favorites

*   Create Android Virtual Device (AVD), for device Samsung Galaxy SIII, running KitKat 4.4.2:

*   Launch Android Studio
*   On screen "Welcome to Android Studio", under section "Configure", select "SDK Manager"
*   On screen "Default Settings", under menu "Appearance & Behavior" > "System Settings" > "Android SDK":

*   On tab "SDK Platforms", select checkbox for Name "Android 4.4.2"
*   Select button "Apply"
*   On screen "Confirm Change", select button "OK"
*   On screen "SDK Quickfix Installation", wait until Android Studio completes installing the requested components, then select button "Finish"

*   On screen "Default Settings", under menu "Appearance & Behavior" > "System Settings" > "Android SDK", select link "Launch Standalone SDK Manager"
*   On screen "Android SDK Manager", install KitKat 4.4.2 packages

*   Deselect (for now) packages selected by default, for Name "Android 6.0 (API 23)"

1.  Android TV ARM EABI v7a System Image
2.  Android TV Intel x86 Atom System Image
3.  Android Wear ARM EABI v7a System Image
4.  Android Wear Intel x86 Atom System Image
5.  ARM EABI v7a System Image
6.  Intel x86 Atom\_64 System Image
7.  Intel x86 Atom System Image

*   Select the following packages for Name "Android 4.4.2 (API 19)"

1.  Samples for SDK
2.  ARM EABI v7a System Image
3.  Intel x86 Atom System Image
4.  Google APIs (x86 System Image)
5.  Google APIs (ARM System Image)

*   Leave "Extras > Android Support Library" checked (note: currently Rev 23.1.1)
*   Select button "Install 6 packages"
*   On screen "Choose Packages to Install":

*   Select radio button "Accept License"
*   Select button "Install" (note: the window will close, returning you to the Android SDK Manager")

*   Wait for packages to download and install

*   On screen "Android SDK Manager", create the AVD:

*   Select menu item Tools > "Manage AVDs..."
*   On screen "Android Virtual Device (AVD) Manager:"

*   Select tab "Device Definitions"
*   Select button "Create Device..."
*   On screen "Create New Device":

*   Name: Samsung\_Galaxy\_S3\_KitKat
*   Screen Size (in): 4.8
*   Resolution (px): 720 x 1280
*   Sensors--Check the checkboxes, for the following

*   Accelerometer: Checked
*   Gyroscope: Checked
*   GPS: Checked
*   Proximity Sensor: Checked

*   Camera:

*   Front: Checked
*   Rear: Checked

*   Input:

*   Keyboard: Checked
*   Select "No Nav" radio button (note: this will uncheck disabled checkboxes "Navigation", at right, in section "Device States; just ignore)

*   RAM: 512
*   Size: normal
*   Screen ratio: long
*   Density: xhdpi
*   Buttons: Hardware
*   Device States:

*   Portrait: 

*   Enabled: Checked
*   Navigation: Unchecked

*   Landscape: 

*   Enabled: Checked
*   Navigation: Unchecked

*   Portrait with keyboard (Disabled):

*   Enabled: Checked (Disabled):
*   Navigation: Checked (Disabled):

*   Landscape with keyboard (Disabled):

*   Enabled: Checked (Disabled)
*   Navigation: Unchecked (Disabled)

*   Override the existing device with the same name: disabled or checked, if enbabled

*   Select tab "Android Virtual Devices"
*   Select button "Create"
*   On screen "Create new Android Virtual Device (AVD)":

*   AVD Name: AVD\_For\_Samsung\_Galaxy\_S3\_KitKat
*   Target: Android 4.4.2 - API Level 19
*   CPU/ABI: Intel Atom (x86)
*   Keyboard: 

*   Hardware keyboard present (Checked)

*   Skin: No skin
*   Front camera: Webcam0
*   Rear camera: None
*   Memory Options:

*   RAM: 0
*   VM Heap: 64

*   Internal Storage: 200 MiB
*   SD Card: Blank
*   Emulation Options:

*   Snapshot: Unchecked
*   Use Host GPU: Unchecked

*   Override the existing AVD with the same name: disabled or checked, if enbabled
*   Select button "OK"
*   On screen "Android Virtual Devices Manager", which shows the result of creating the AVD, select button "OK"

*   Close screen "Android Virtual Device (AVD) Manager"

*   Create a new Android Project

*   Launch Android Studio
*   On screen "Welcome to Android Studio", select "Start a new Android Studio project"
*   On screen "Configure your new project":

*   Application name: HelloWorld
*   Company Domain: iokevins.com
*   Project location: /home/k/AndroidStudioProjects/HelloWorld
*   Select button "Next"

*   On screen "Select the form factors your app will run on":

*   Phone and tablet: Checked
*   Minimum SDK: API 15: Android 4.0.3 (IceCreamSandwich)
*   Leave other checkboxes unchecked
*   Select button "Next"

*   On screen "Add an activity to Mobile":

*   Select "Blank Activity"
*   Select button "Next"

*   On screen "Customize the Activity"

*   Activity Name: MyActivity
*   Layout Name: activity\_my
*   Title: MyActivity
*   Menu Resource Name: menu\_my
*   Use a Fragment: Unchecked
*   Select button "Finish"

*   Wait for the Android Studio IDE to display
*   Select menu item Run > "Run App"
*   On screen "Device Chooser":

*   Launch emulator: Selected
*   Android virtual device: "AVD\_For\_Samsung\_Galaxy\_S3\_KitKat
*   Select button "OK"

*   Note: a popup window may ask whether to continue waiting; if so, select "Wait"
*   On the AVD:

*   Swipe right to login
*   HelloWorld app appears

*   Close the AVD

### Resources

[How to Install Oracle Java and Android Studio on a 64-Bit Debian 8.0 Cinnamon (Jessie)](http://ridz1ba.blogspot.com/2015/07/how-to-install-oracle-java-and-android.html)