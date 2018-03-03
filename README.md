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
