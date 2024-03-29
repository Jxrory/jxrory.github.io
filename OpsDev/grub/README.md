# Grub 使用

## grub 安装 - Ubuntu

NOTICE:

- `/dev/sdb`: 硬盘（U 盘）设备;
- `/media/u`: 硬盘（U 盘）挂载点;

```sh
sudo grub-install --root-directory=/media/u /dev/sdb
```

## grub 配置

```sh
# 设置一些全局环境变量
# 当开机时选中某个菜单项启动时，该菜单的title将被赋值给chosen变量。该变量一般只用于引用，而不用于修改。
# #set chosen=
# grub2加载的core.img的目录路径，是绝对路径，即包括了设备名的路径，如(hd0,gpt1)/boot/grub2/。该变量值不应该修改
# #set cmdpath=
# default指定默认菜单时，可使用菜单的title，也可以使用菜单的id，或者数值顺序，当使用数值顺序指定default时，从0开始计算
set default=0
# 设置菜单等待超时时间，设置为0时将直接启动默认菜单项而不显示菜单，设置为"-1"时将永久等待手动选择。
set timeout=-1
# 当默认菜单项启动失败，则使用该变量指定的菜单项启动，指定方式同default，可使用数值(从0开始计算)、title或id指定。
# #set fallback=1
# 指定该平台是"pc"还是"efi"，pc表示的就是传统的bios平台。该变量不应该被修改，而应该被引用，例如用于if判断语句中。
# #set grub_platform=
# 在grub启动的时候，grub自动将/boot/grub2目录的绝对路径赋值给该变量
# #set prefix=(hd0,gpt1)/boot/grub2/
# 该变量指定根设备的名称，使得后续使用从"/"开始的相对路径引用文件时将从该root变量指定的路径开始。一般该变量是grub启动的时候由grub根据prefix变量设置而来的。
# set root='hd0,msdos1'

insmod fat
insmod loopback
insmod iso9660

# `9744-CFE5` 为 U盘的 UUID
search --no-floppy --fs-uuid --set=hdroot 9744-CFE5

# 设置变量:  `isopath` iso 镜像存放的地方
set isopath="/iso"

# 启动配置项
menuentry 'ubuntu-22.04.3-live-server-amd64.iso' {
  set isofile=${isopath}"/ubuntu-22.04.3-live-server-amd64.iso"
  loopback loop (${hdroot})${isofile}
  set root=(loop)

  linux /casper/vmlinuz boot=casper iso-scan/filename=${isofile} quiet noeject noprompt splash
  initrd /casper/initrd
}
```

配置样例：

- [grub-learn.cfg](./config/grub-learn.cfg)
- [grub-iso-installer.cfg](./config/grub-iso-installer.cfg)
