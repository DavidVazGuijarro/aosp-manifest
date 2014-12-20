AOSP for Xperia
===============

AOSP 5.0 for Xperia devices

Preparing the code
------------------

First we will initialize the aosp repo, execute the following in terminal:
```bash
mkdir aosp
cd aosp
repo init -u https://android.googlesource.com/platform/manifest -b android-5.0.0_r7
```

To setup a tree and build images for the device put the following snippet in 
`.repo/local_manifests/xperia.xml`:

You can find the xperia.xml manifest in this repo. Copy the contents to your empty xperia.xml file.

Building the rom
----------------
Execute the following in terminal to sync sources and build a rom:

Add these patches:
```bash
cd hardware/qcom/bt

git cherry-pick 5a6037f1c8b5ff0cf263c9e63777444ba239a056

cd ../display

git cherry-pick e9e1e3a16144a2410e592f67bab8e24c60df52ea

git revert 0fdae193307fb17bb537598ab62682edd5138b72

cd ../../ril

git fetch https://github.com/adrian-bl-yuga/android_hardware_ril.git 31929dcee6e648ceb9bf4a4924fe6af9c1e6686d && git cherry-pick FETCH_HEAD

cd ../../system/core

git fetch https://github.com/tg-togari-lollipop/android_system_core.git 29fc7b17bb5e7a835b74f8038ff5ebdf4d860fc0 && git cherry-pick FETCH_HEAD

cd ../../external/libnfc-nci/

git fetch https://android.googlesource.com/platform/external/libnfc-nci refs/changes/42/103142/1 && git cherry-pick FETCH_HEAD

cd ../..
```

Then build the rom using the following commands:
```bash
repo sync
. build/envsetup.sh && lunch aosp_xxxx-userdebug
make -j
```