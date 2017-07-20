obj-m += gtp.o

all:
	echo ${KBUILD_EXTRA_SYMBOLS}
	make -C /lib/modules/`uname -r`/build M=$(PWD) modules
	
install:
	install gtp.ko /lib/modules/`uname -r`/kernel/drivers/net/

clean:
	make -C /lib/modules/`uname -r`/build M=$(PWD) clean
