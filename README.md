Usage
=====
build LineageOS 17.0
---------------
navigate into desired directory

initialize repo:

    repo init -u https://github.com/LineageOS/android.git -b lineage-17.0

download manifest: 

    curl https://raw.githubusercontent.com/115ek/manifest/master/amami_lineage_17.0.xml > /your_directory/.repo/local_manifests/amami.xml

sync repo:

    $ repo sync

setup build environment

    $ source build/envsetup.sh

get needed patches:

    apply patches from here: https://github.com/sagit-10-temp/local_manifests/blob/master/picks.sh (too lazy to list them here... big thanks @Arian :) ) This will be removed when all the things become more mature
    
    $ repopick -g https://gerrit.aicp-rom.com -t sony8974_ten
    $ repopick -g https://gerrit.aicp-rom.com -t sony8974_shim_update
    
    Also big thanks @SpiritCroc :)

build:

    brunch amami

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

    $ repopick -g https://gerrit.aicp-rom.com 88139 88145 92246

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
TWRP is built in a minimal environment to save disk space and to avoid a lot of unnecessary things.

navigate into desired directory

initialize repo: 

    repo init -u git://github.com/minimal-manifest-twrp/platform_manifest_twrp_omni.git -b twrp-9.0

download manifest: 

    curl https://raw.githubusercontent.com/115ek/manifest/master/amami_twrp.xml > /your_directory/.repo/local_manifests/amami_twrp.xml

sync repo:

    $ repo sync

get needed patch (this fixes automatic OTA update installation):

    $ repopick -g https://gerrit.omnirom.org 35313

build:

    export ALLOW_MISSING_DEPENDENCIES=true
    . build/envsetup.sh && lunch omni_amami-eng
    mka recoveryimage
