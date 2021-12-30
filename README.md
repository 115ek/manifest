Usage
=====
build LineageOS 19.0
---------------
navigate into desired directory

initialize repo:

    repo init -u https://github.com/LineageOS/android.git -b lineage-19.0

download manifest:

    curl https://raw.githubusercontent.com/115ek/manifest/master/amami_lineage_19.0.xml > /your_directory/.repo/local_manifests/amami.xml

sync repo:

    $ repo sync

setup build environment

    $ source build/envsetup.sh

apply needed patches:

    $ repopick -P system/bpf 320591
    $ repopick -P system/netd 320592
    $ repopick -P system/tools/mkbootimg 319780
    $ repopick -P art 318097
    $ repopick -f 287706 -P external/perfetto
    $ repopick 317298 317300 317301

apply this patch in `hardware/qcom-caf/msm8974/display`:
```patch
From a820dd37a8fd4bc95bb3502ce2219254f78d7adc Mon Sep 17 00:00:00 2001
From: Kyle Harrison <khwebmail@gmail.com>
Date: Sun, 19 Dec 2021 16:49:04 +0000
Subject: [PATCH] hwc: Update dependencies for S

ld.lld: error: undefined symbol: SkFILEWStream::SkFILEWStream(char const*)
ld.lld: error: undefined symbol: SkEncodeImage(SkWStream*, SkPixmap const&, SkEncodedImageFormat, int)
ld.lld: error: undefined symbol: SkFILEWStream::~SkFILEWStream()

- Builing against libhwui no longer fulfils the skia dependency.
- Link against the smaller libskia_renderengine library which does not require all of the codec dependencies of the full libskia.

Change-Id: Ib77f379859c6af9acf787b98fdd848959a54c69f
---
 libhwcomposer/Android.mk | 3 ++-
 1 file changed, 2 insertions(+), 1 deletion(-)

diff --git a/libhwcomposer/Android.mk b/libhwcomposer/Android.mk
index 8f1c29e10a..3bd29c5781 100644
--- a/libhwcomposer/Android.mk
+++ b/libhwcomposer/Android.mk
@@ -23,7 +23,8 @@ LOCAL_CFLAGS                  := $(common_flags) -DLOG_TAG=\"qdhwcomposer\" -Wno
                                  -Wno-float-conversion -Wno-unused-parameter
 
 ifeq ($(TARGET_USES_QCOM_BSP),true)
-LOCAL_SHARED_LIBRARIES += libhwui
+LOCAL_STATIC_LIBRARIES += libskia_renderengine
+LOCAL_SHARED_LIBRARIES += libnativewindow libGLESv2 libpng
 ifeq ($(GET_FRAMEBUFFER_FORMAT_FROM_HWC),true)
     LOCAL_CFLAGS += -DGET_FRAMEBUFFER_FORMAT_FROM_HWC
 endif
-- 
2.34.1
```

build:

    brunch amami


Thanks @chil360
more info here: https://github.com/chil360/lineage_osprey

build LineageOS 18.1
---------------

Attention! 18.1 is now build from https://github.com/lin18-microG/local_manifests
Below patches are no longer required when building from there.

navigate into desired directory

initialize repo:

    repo init -u https://github.com/LineageOS/android.git -b lineage-18.1

download manifest:

    curl https://raw.githubusercontent.com/115ek/manifest/master/amami_lineage_18.1.xml > /your_directory/.repo/local_manifests/amami.xml

sync repo:

    $ repo sync

setup build environment

    $ source build/envsetup.sh

apply needed patches:

    $ repopick 310331 # Settings: Display NFC settings correctly
    $ cd device/sony/msm8974-common
    $ git fetch http://gerrit.aicp-rom.com/AICP/device_sony_msm8974-common refs/changes/28/109528/4 && git checkout FETCH_HEAD
    $ cd ../../..
    $ cd device/sony/rhine-common
    $ git fetch http://gerrit.aicp-rom.com/AICP/device_sony_rhine-common refs/changes/31/109531/7 && git checkout FETCH_HEAD

in device/sony/rhine-common apply the following patch:
```
diff --git a/rhine.mk b/rhine.mk
index 17d35aa8..cacf5a39 100644
--- a/rhine.mk
+++ b/rhine.mk
@@ -12,7 +12,7 @@
    # See the License for the specific language governing permissions and
    # limitations under the License.
    
-$(call inherit-product, vendor/aicp/build/target/product/product_launched_with_j_mr2.mk)
+$(call inherit-product, vendor/lineage/build/target/product/product_launched_with_j_mr2.mk)
    
    # inherit from msm8974-common
    $(call inherit-product, device/sony/msm8974-common/msm8974.mk)
```

build:

    brunch amami

build LineageOS 17.1
---------------
Attention! 17.1 is now build from https://github.com/lin17-microG/local_manifests

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
