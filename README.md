属国
对于Windows/MAC OS/其他Linux发行版:

手动安装Docker或使用Ubuntu虚拟机

对于Ubuntu 20.04:

sudo apt update
sudo apt upgrade
sudo apt install build-essential uuid-dev iasl git nasm gcc-aarch64-linux-gnu python3-distutils python3-pil python3-git gettext
如果您使用的是GCC 11+，请修改edk2/BaseTools/Source/C/Makefiles/header.makefile

diff --git a/BaseTools/Source/C/Makefiles/header.makefile b/BaseTools/Source/C/Makefiles/header.makefile
index 0df728f..247c917 100644
--- a/BaseTools/Source/C/Makefiles/header.makefile
+++ b/BaseTools/Source/C/Makefiles/header.makefile
@@ -92,7 +92,7 @@ BUILD_CFLAGS = -MD -fshort-wchar -fno-strict-aliasing -fwrapv \
 -Wno-unused-result -nostdlib -g
 else
 BUILD_CFLAGS = -MD -fshort-wchar -fno-strict-aliasing -fwrapv \
--fno-delete-null-pointer-checks -Wall -Werror \
+-fno-delete-null-pointer-checks -Wall \^M
 -Wno-deprecated-declarations -Wno-stringop-truncation -Wno-restrict \
 -Wno-unused-result -nostdlib -g
 endif
建筑物
1.克隆此项目

git clone https://github.com/hejianwei889/sdm845.git --depth=1
cd edk2-sdm845
2.1构建这个项目(仅在linux上)

bash build.sh --device DEVICE
2.2对于Macos/Windows(可以使用docker)

docker-compose run edk2 ./build.sh -d DEVICE
3.启动映像

fastboot boot boot_DEVICE.img
(设备是你手机的代号。)

此外，您可以刷新映像进行恢复，以实现双启动。

fastboot flash recovery boot_DEVICE.img
信用
fxsheep为了他的原创edk2-sagit

strongtz维护叛离项目

BigfootACA对于构建脚本

Lemon_Ice和NTAuthority为指导和一些blobs

@Freak2112, TAO_Croatia和废物努力进行测试和调试

NekokeCore用于修复内存映射
