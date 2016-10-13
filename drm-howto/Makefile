ifeq ($(CROSS),)
FLAGS=`pkg-config --cflags --libs libdrm`
else
FLAGS=-L $(SYSROOT)/usr/lib -ldrm -I$(SYSROOT)/usr/include/libdrm -I$(SYSROOT)/usr/include
endif

FLAGS+=-Wall -O0 -g
FLAGS+=-D_FILE_OFFSET_BITS=64

help:
	@echo '  Native compile:'
	@echo 'make all CROSS='
	@echo '  Cross-compile:'
	@echo 'make all CROSS=cross-compile-prefix- SYSROOT=/path/to/target/sysroot'
	@echo ''
	@echo '  Example for 64-bit petalinux cross-compile:'
	@echo 'make all CROSS=aarch64-linux-gnu- SYSROOT=$$PETALNX_WD/build/linux/rootfs/stage/'

all:
	$(CROSS)gcc -o modeset modeset.c $(FLAGS)
	$(CROSS)gcc -o modeset-double-buffered modeset-double-buffered.c $(FLAGS)
	$(CROSS)gcc -o modeset-vsync modeset-vsync.c $(FLAGS)
