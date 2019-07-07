Usage
=====
build LineageOS 16.0
---------------
navigate into desired directory

initialize repo:

    repo init -u https://github.com/LineageOS/android.git -b lineage-16.0

download manifest: 

    curl https://raw.githubusercontent.com/115ek/manifest/master/amami_lineage_16.0.xml > /your_directory/.repo/local_manifests/amami.xml

sync repo:

    $ repo sync

setup build environment

    $ source build/envsetup.sh

get needed patches:

    $ repopick -g https://review.lineageos.org 248682
    $ repopick -g https://gerrit.aicp-rom.com 88139 88145 92245 92246

build:

    brunch amami

build LineageOS 15.1
---------------
Attention! 15.1 is now build from https://github.com/lin15-microG/local_manifests
(you're still able to use this manifest, too)
navigate into desired directory

initialize repo:

    repo init -u https://github.com/LineageOS/android.git -b lineage-15.1

download manifest: 

    curl https://raw.githubusercontent.com/115ek/manifest/master/amami.xml > /your_directory/.repo/local_manifests/amami.xml

sync repo:

    $ repo sync

build:

    . build/envsetup.sh
    brunch amami

build TWRP
----------
download manifest: 

    curl https://raw.githubusercontent.com/115ek/manifest/master/amami_twrp.xml > /your_directory/.repo/local_manifests/amami_twrp.xml

sync repo:

    $ repo sync

build:

    . build/envsetup.sh
    lunch

choose **lineage_amami-eng** here!
    
    mka recoveryimage
