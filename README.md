# embeddedTS Yocto BSP

A very light-weight BSP intended to produce images for our platforms using core Poky, OpenEmbedded, and our own meta-ts layer.

The configuration of our BSP is based around using `kas` for management of configurations.

See files in the `kas-includes/` for details on what each of these brings to the final configuration.

Configuration files in `kas-configurations/` are organized by CPU series (`tsimx6/`, `tsa38x/`, `tsimx28/`, `tsimx6ul/`, etc.) and then by individual platform model.


## Building with this BSP
### Clone the repository
```
git clone https://github.com/embeddedTS/ts-oe-bsp
cd ts-oe-bsp
```

### Install kas
```
pip install -r requirements.txt
```

### Build
```
kas build kas-configs/<series>/<model>.yml
```

### Using Generated Images
A number of images may be generated from any specific configuration file. Usually this is `core-image-cmdline-full-ts` only when building for platforms without a display of any kind; as well as `core-image-weston-ts` for platforms that offer a display (via integrated touchpanel or external display output).

These images are output to `build/tmp/deploy/images/<model>/` and can be loaded on to the target using the instructions from that device's manual.

### Building an External Toolchain
It is also possible to build a toolchain.  To build the toolchain:
```
kas build kas-configs/<series>/<model>.yml -- -c populate_sdk
```
This will build the toolchain install script in `build/tmp/deploy/sdk/poky-glibc-x86_64-<image>-<arch>-<model>-toolchain-<version>.sh`

Executing this script installs the toolchain into `/opt/poky/<version>`.  To use it to build, first `source /opt/poky/<version>/environment-setup-<arch>-poky-linux-gnueabi` then run make,cmake, meson, etc.  It will build arm binaries using same compiler and libraries used in the yocto image, binaries can be copied over to the eTS board.

### Building with systemd
To build an image using systemd instead of sysvinit, apply the systemd.yml override:
```
kas build kas-configs/<series>/<model>.yml:kas-includes/systemd.yml
```
