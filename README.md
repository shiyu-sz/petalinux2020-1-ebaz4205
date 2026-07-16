
source /opt/pkg/petalinux/2020.1/settings.sh

petalinux-create -t project --template zynq -n ebaz4205

petalinux-config --get-hw-description=./vivado

petalinux-build