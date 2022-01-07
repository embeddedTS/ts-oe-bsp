TS Yocto BSP
=========

Step 1: Install repo

```bash
mkdir ~/bin
curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo`
chmod a+x ~/bin/repo
export PATH=${PATH}:~/bin
```

Step 2: Checkout Yocto

```bash
mkdir ts-bsp
cd ts-bsp
repo init -u https://github.com/embeddedTS/ts-oe-bsp.git -b zeus
repo sync
```

Step 3: Set Build Env

```bash
export MACHINE="tsimx6"
source sources/poky/oe-init-build-env 
```

Step 4: Set bitbake layers (conf/bblayers.conf)
```
# POKY_BBLAYERS_CONF_VERSION is increased each time build/conf/bblayers.conf
# changes incompatibly
POKY_BBLAYERS_CONF_VERSION = "2"

BBPATH = "${TOPDIR}"
BSPDIR := "${@os.path.abspath(os.path.dirname(d.getVar('FILE', True)) + '/../..')}"

BBFILES ?= ""

BBLAYERS ?= " \
  ${BSPDIR}/sources/poky/meta \
  ${BSPDIR}/sources/poky/meta-poky \
  ${BSPDIR}/sources/poky/meta-yocto-bsp \
  ${BSPDIR}/sources/meta-freescale \
  ${BSPDIR}/sources/meta-freescale-3rdparty \
  ${BSPDIR}/sources/meta-freescale-distro \
  ${BSPDIR}/sources/meta-openembedded/meta-oe \
  ${BSPDIR}/sources/meta-openembedded/meta-python \
  ${BSPDIR}/sources/meta-openembedded/meta-multimedia \
  ${BSPDIR}/sources/meta-openembedded/meta-gnome \
  ${BSPDIR}/sources/meta-openembedded/meta-networking \
  ${BSPDIR}/sources/meta-ts \
  ${BSPDIR}/sources/meta-qt5 \
  "
```

Step 5: Download/Compile image:

```bash
bitbake ts-x11-image
```
