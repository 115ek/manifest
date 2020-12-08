Usage
=====
build LineageOS 18.0
---------------
navigate into desired directory

initialize repo:

    repo init -u https://github.com/LineageOS/android.git -b lineage-18.0

download manifest:

    curl https://raw.githubusercontent.com/115ek/manifest/master/amami_lineage_18.0.xml > /your_directory/.repo/local_manifests/amami.xml

sync repo:

    $ repo sync

setup build environment

    $ source build/envsetup.sh

get needed patches:

    $ repopick 295701 292788 289841 286185 292244 # legacy support, adb, ...
    $ repopick 287706 -P external/perfetto
    $ repopick -g https://gerrit.aicp-rom.com 104256 104257 # vendor
    $ repopick -g https://gerrit.aicp-rom.com 104527 # kernel
    $ repopick -g https://gerrit.aicp-rom.com 105493 105494 105495 105496 # sony-common
    $ repopick -g https://gerrit.aicp-rom.com 104258 104259 104528 104529 104531 104532 105898 106137 106233 # rhine-common
    $ repopick -g https://gerrit.aicp-rom.com 104521 104522 104523 104525 104996 104997 104998 105894 105895 105897 106066 106067 106096 106145 106146 106147 # 8974-common
    $ repopick -g https://gerrit.aicp-rom.com 105818 -P system/core
    $ repopick -g https://gerrit.aicp-rom.com 105646 -P frameworks/native
    $ repopick -g https://gerrit.aicp-rom.com 105644 -P build/make
    $ repopick -g https://gerrit.aicp-rom.com 105645 -P build/soong
    $ repopick -g https://gerrit.aicp-rom.com 105817 -P vendor/lineage

build:

    brunch amami

build LineageOS 17.1
---------------
navigate into desired directory

initialize repo:

    repo init -u https://github.com/LineageOS/android.git -b lineage-17.1

download manifest: 

    curl https://raw.githubusercontent.com/115ek/manifest/master/amami_lineage_17.1.xml > /your_directory/.repo/local_manifests/amami.xml

sync repo:

    $ repo sync

setup build environment

    $ source build/envsetup.sh

get needed patches:

    $ repopick -g https://gerrit.aicp-rom.com 102576

build:

    brunch amami

build LineageOS 16.0
---------------
Attention! 16.0 is now build from https://github.com/lin16-microG/local_manifests
(you're still able to use this manifest, too)

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

set up build env:

    $ export ALLOW_MISSING_DEPENDENCIES=true
    $ source build/envsetup.sh

get needed patch (this fixes automatic OTA update installation):

    $ repopick -g https://gerrit.twrp.me 1673 1990

build:

    $ lunch omni_amami-eng
    $ mka recoveryimage
