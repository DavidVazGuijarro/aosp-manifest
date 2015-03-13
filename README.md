AOSP for Xperia
===============

AOSP 5.0 for Xperia devices

Preparing the code
------------------

First we will initialize the aosp repo, execute the following in terminal:
```bash
mkdir aosp
cd aosp
repo init -u https://android.googlesource.com/platform/manifest -b android-5.1.0_r1
```

To setup a tree and build images for the device put the following snippet in 
`.repo/local_manifests/xperia.xml`:

You can find the xperia.xml manifest in this repo. Copy the contents to your empty xperia.xml file.

Multirom extras/libbootimg
--------------------------

`git clone https://github.com/Tasssadar/multirom.git system/extras/multirom
cd system/extras/multirom
git submodule update --`

It also needs libbootimg:

`git clone https://github.com/Tasssadar/libbootimg.git system/extras/libbootimg`

Building the rom
----------------
Execute the following in terminal to sync sources and build a rom:

Add these patches:
```bash
cd hardware/qcom/bt

git cherry-pick 5a6037f1c8b5ff0cf263c9e63777444ba239a056

cd ../display

git revert ab05b00fefd34a761dfaf1ccaf8ad14d325873f4

cd ../../../external/libnfc-nci/

git fetch https://android.googlesource.com/platform/external/libnfc-nci refs/changes/42/103142/1 && git cherry-pick FETCH_HEAD

git fetch https://android.googlesource.com/platform/external/libnfc-nci refs/changes/23/103123/1 && git cherry-pick FETCH_HEAD

git fetch https://android.googlesource.com/platform/external/libnfc-nci refs/changes/51/97051/1 && git cherry-pick FETCH_HEAD

cd ../../hardware/libhardware/

git fetch https://android.googlesource.com/platform/hardware/libhardware refs/changes/21/103221/2 && git cherry-pick FETCH_HEAD

cd ../../ril

git fetch https://github.com/adrian-bl-yuga/android_hardware_ril.git 31929dcee6e648ceb9bf4a4924fe6af9c1e6686d && git cherry-pick FETCH_HEAD

cd ../../system/core

git fetch https://github.com/tg-togari-lollipop/android_system_core.git 29fc7b17bb5e7a835b74f8038ff5ebdf4d860fc0 && git cherry-pick FETCH_HEAD

cd ../..
```

Then build the rom using the following commands:
```bash
repo sync
. build/envsetup.sh && lunch aosp_xxxx-userdebug
make -j
```