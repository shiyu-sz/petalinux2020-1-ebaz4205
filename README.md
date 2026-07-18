
# EBAZ4205 PetaLinux 2020.1

## Build

```sh
source /tools/petalinux-v2020.1/settings.sh

petalinux-config --get-hw-description=./vivado

petalinux-build -x mrproper -f

petalinux-build

# sd
petalinux-package --boot --u-boot --force --fpga 

# flash
petalinux-package --boot --force \
    --boot-device flash \
    --fsbl images/linux/zynq_fsbl.elf \
    --fpga images/linux/system.bit \
    --u-boot images/linux/u-boot.elf \
    --dtb images/linux/system.dtb --load 0x00100000 \
    --kernel images/linux/image.ub --load 0x01000000 \
    --output images/linux/BOOT-all.BIN

program_flash \
    -f images/linux/BOOT-all.BIN \
    -offset 0 \
    -flash_type nand-x8 \
    -fsbl images/linux/zynq_fsbl.elf \
    -erase_sector 131072 \
    -verify
```
