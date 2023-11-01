sudo apt update && sudo apt -y upgrade && sudo apt -y install gperf gcc-multilib gcc-10-multilib g++-multilib g++-10-multilib libc6-dev lib32ncurses5-dev x11proto-core-dev libx11-dev tree lib32z-dev libgl1-mesa-dev libxml2-utils xsltproc bc ccache lib32readline-dev lib32z1-dev liblz4-tool libncurses5-dev libsdl1.2-dev libwxgtk3.0-gtk3-dev libxml2 lzop pngcrush schedtool squashfs-tools imagemagick libbz2-dev lzma ncftp qemu-user-static libstdc++-10-dev libncurses5 python3

mkdir ~/bin && curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo && chmod a+x ~/bin/repo && sudo ln -sf ~/bin/repo /usr/bin/repo

cd workspace
echo "workspace-folder=$(pwd)" >> $GITHUB_OUTPUT
git config --global user.name "Nico170420" && git config --global user.email "b170420nc@gmail.com"
repo init --depth=1 -u https://github.com/minimal-manifest-twrp/platform_manifest_twrp_aosp -b twrp-12.1

repo sync -j$(nproc --all) --force-sync

git clone https://github.com/TeamWin/android_device_asus_I003D -b android-12.1 ./device/asus/I003D


bash ${GITHUB_WORKSPACE}/scripts/convert.sh <DEVICE_PATH>/<BUILD_TREE_VALUE>.dependencies
repo sync -j$(nproc --all)

source build/envsetup.sh
export ALLOW_MISSING_DEPENDENCIES=true
lunch <MAKEFILE_NAME>-eng && make clean && make <BUILD_TARGET>image -j$(nproc --all)
