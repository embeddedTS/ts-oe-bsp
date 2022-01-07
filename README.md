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
repo init -u https://github.com/embeddedTS/ts-oe-bsp -b morty
repo sync
```

Step 3: Set Build Env

```bash
export MACHINE="tsimx6"
export DISTRO="poky"
source ./setup-environment build
```

Step 4: Set bitbake layers (conf/bblayers.conf)
```
POKY_BBLAYERS_CONF_VERSION = "2"

BBPATH = "${TOPDIR}"
BSPDIR := "${@os.path.abspath(os.path.dirname(d.getVar('FILE', True)) + '/../..')}"

BBFILES ?= ""
BBLAYERS = " \
  ${BSPDIR}/sources/poky/meta \
  ${BSPDIR}/sources/poky/meta-poky \
  \
  ${BSPDIR}/sources/meta-openembedded/meta-oe \
  ${BSPDIR}/sources/meta-openembedded/meta-multimedia \
  ${BSPDIR}/sources/meta-openembedded/meta-networking \
  ${BSPDIR}/sources/meta-openembedded/meta-python \
  ${BSPDIR}/sources/meta-openembedded/meta-gnome \
  \
  ${BSPDIR}/sources/meta-freescale \
  ${BSPDIR}/sources/meta-freescale-3rdparty \
  ${BSPDIR}/sources/meta-freescale-distro \
  \
  ${BSPDIR}/sources/meta-ts \
  ${BSPDIR}/sources/meta-qt5 \
  ${BSPDIR}/sources/meta-browser \
"
```

Step 5 (Optional): Set additional conf/local.conf options:
```
LICENSE_FLAGS_WHITELIST = "commercial_libav commercial"
DISTRO_FEATURES_remove = "wayland "
DISTRO_FEATURES_append = " x11 systemd"
DISTRO_FEATURES_BACKFILL_CONSIDERED = "sysvinit"
VIRTUAL-RUNTIME_init_manager = "systemd"
VIRTUAL-RUNTIME_initscripts = ""
```

Step 6: Download/Compile image:

```bash
bitbake ts-x11-image
```
