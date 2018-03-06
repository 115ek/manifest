Usage
=====
navigate into desired directory

initialize repo:

    repo init -u https://github.com/LineageOS/android.git -b lineage-15.1

build LineageOS
---------------
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
