TS Yocto BSP
=========

Step 1: Install repo

```bash
mkdir ~/bin
curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo
export PATH=${PATH}:~/bin
```

Step 2: Checkout Yocto

```bash
mkdir ts-bsp
cd ts-bsp
repo init -u https://github.com/embeddedTS/ts-oe-bsp.git -b hardknott
repo sync
```

Step 3: Set Build Env

```bash
# For embeddedTS i.MX6 based devices
export TEMPLATECONF=$(pwd)/sources/meta-ts/conf/tsimx6_conf
source sources/poky/oe-init-build-env 
```

Step 4: Download/Compile image:

```bash
bitbake ts-x11-image
```
