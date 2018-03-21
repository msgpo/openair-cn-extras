# GTP Integration Off-Tree Build

## Usage

### gtp.ko

```
make
make install  # this overwrites the old gtp.ko

make -C /lib/modules/`uname -r`/build M=$PWD
sudo cp gtp.ko /lib/modules/`uname -r`/kernel/drivers/net/gtp.ko
```
