Usage
=====
build LineageOS 18.1
---------------
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
