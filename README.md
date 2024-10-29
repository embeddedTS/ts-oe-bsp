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
kas build kas-configurations/<series>/<model>.yml
```

### Using Generated Images
A number of images may be generated from any specific configuration file. Usually this is `core-image-cmdline-full-ts` only when building for platforms without a display of any kind; as well as `core-image-weston-ts` for platforms that offer a display (via integrated touchpanel or external display output).

These images are output to `build/tmp/deploy/images/<model>/` and can be loaded on to the target using the instructions from that device's manual.

### Building an External Toolchain
It is also possible to build a toolchain, DOCUMENT THIS
