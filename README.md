TS Yocto BSP
=========

Step 1: Install repo

$: mkdir ~/bin
$: curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
$: chmod a+x ~/bin/repo
$: export PATH=${PATH}:~/bin

Step 2: Checkout source
$: mkdir ts-bsp
$: cd ts-bsp
$: repo init -u https://github.com/embeddedarm.com/ts-oe-bsp -b dizzy
$: repo sync

Step 3: Build
$: source ./setup-environment build

We provide 2 images with common packages:

# For X11 + QT + other common utilities
$: bitbake ts-x11-image

# Or for a headless system
$: bitbake ts-headless-image

