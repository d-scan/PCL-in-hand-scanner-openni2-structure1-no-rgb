# PCL's in_hand_scanner tutorial for openni2 and Structure Sensor

Structure Sensor does not have a rgb camera like the original Kinect has.

Original tutorial page can be found here:
http://pointclouds.org/documentation/tutorials/in_hand_scanner.php

This port itself it a port from https://github.com/EricAlex/in_hand_scanner

## Preparation

This has only been testen  MacOS 10.14

### Install QT5

```
brew install qt5
```

### Install OpenNI2 from Occipital

Download **OpenNI2** fork from Occipital (OpenNI-MacOSX-x64-2.2) and place in
/Applications (/Applications/OpenNI-MacOSX-x64-2.2)

### Install PCL

Compile PCL from source with support for OpenNI2. I followed this tutorial:
http://robotica.unileon.es/index.php/PCL/OpenNI_tutorial_1:_Installing_and_testing

## Build instructions as a script

```bash
# step 1: set clone directory
export INHANDROOTDIR=/tmp/inhandscannerbymipmip

# step 2: remove dir if exists
rm -Rf $INHANDROOTDIR

# step 3: clone source

mkdir -p $INHANDROOTDIR
rmdir $INHANDROOTDIR
git clone mipmip/PCL-in-hand-scanner-openni2-structure1-no-rgb $INHANDROOTDIR

# step 4: set exports for OPENNI2:
export OPENNI2_REDIST=/Applications/OpenNI-MacOSX-x64-2.2/Redist/
export OPENNI2_REDIST_LIB=/Applications/OpenNI-MacOSX-x64-2.2/Redist/libOpenNI2.dylib
export OPENNI2_INCLUDE=/Applications/OpenNI-MacOSX-x64-2.2/Include

# step 5: configure with cmake
# see: https://github.com/totakke/homebrew-openni2/issues/1#issuecomment-141933378

cd  $INHANDROOTDIR && cmake -DOPENNI2_LIBRARY=$OPENNI2_REDIST_LIB -DOPENNI2_INCLUDE_DIR=$OPENNI2_INCLUDE -DCMAKE_BUILD_TYPE=Release .

# step 6: build
cd  $INHANDROOTDIR && make

# step 7: copy lib to current dir
cd  $INHANDROOTDIR && cp $OPENNI2_REDIST_LIB ./

# step 8: test
cd  $INHANDROOTDIR && ./pcl_in_hand_scanner
```


