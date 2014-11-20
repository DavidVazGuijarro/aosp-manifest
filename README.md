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

```bash
repo sync
. build/envsetup.sh && lunch aosp_xxxx-userdebug
make -j
```