# First make a folder and go to the folder.

1: sync twrp repo :

repo init -u https://github.com/minimal-manifest-twrp/platform_manifest_twrp_omni.git -b twrp-9.0 && repo sync

2: Clone device tree: in device/manufacturer/device_name folder
Example: device/samsung/a22

git clone https://github.com/Al-Noman-12/a225fx_device_tree device/samsung/a22

. build/envsetup.sh

lunch omni_a22-eng
