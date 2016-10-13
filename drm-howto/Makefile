ifeq ($(CROSS),)
FLAGS=`pkg-config --cflags --libs libdrm`
else
FLAGS=-L $(SYSROOT)/usr/lib -ldrm -I$(SYSROOT)/usr/include/libdrm -I$(SYSROOT)/usr/include
endif

ifneq ($(DRM_FORMAT),)
FLAGS+=-D MODESET_DRM_FORMAT=DRM_FORMAT_$(DRM_FORMAT)
endif


FLAGS+=-Wall -O0 -g
FLAGS+=-D_FILE_OFFSET_BITS=64

help:
	@echo '  Native compile:'
	@echo 'make all CROSS='
	@echo '  Cross-compile:'
	@echo 'make all CROSS=cross-compile-prefix- SYSROOT=/path/to/target/sysroot'
	@echo '  Specify pixel format:'
	@echo 'make all DRM_FORMAT=ABGR8888 # see: <drm/drm_fourcc.h> and run "modetest -M DRM_DRIVER -p" for supported formats'
	@echo ''
	@echo '  Example for 64-bit petalinux cross-compile:'
	@echo 'make all CROSS=aarch64-linux-gnu- SYSROOT=$$PETALNX_WD/build/linux/rootfs/stage/ DRM_FORMAT=ABGR8888'

all:
	$(CROSS)gcc -o modeset modeset.c $(FLAGS)
	$(CROSS)gcc -o modeset-double-buffered modeset-double-buffered.c $(FLAGS)
	$(CROSS)gcc -o modeset-vsync modeset-vsync.c $(FLAGS)
