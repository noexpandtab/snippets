Based on:
 * https://wiki.osdev.org/GCC_Cross-Compiler

install the following packages
 * bison
 * build-essential
 * flex
 * libgmp3-dev
 * libmpc-dev
 * libmpfr-dev
 * libncurses-dev
 * texinfo

download the sources

	git clone git://sourceware.org/git/binutils-gdb.git
	git clone git://gcc.gnu.org/git/gcc.git

compile the sources

	PREFIX="/tmp/opt/cross"
	TARGET=i686-elf
	PATH="$PREFIX/bin:$PATH"
	
	mkdir binutils-gdb/build
	cd binutils-gdb/build
	../configure -target=$TARGET --prefix="$PREFIX" --with-sysroot --disable-nls --disable-werror --enable-tui
	make
	make install
	cd ..
	
	mkdir gcc/build
	cd gcc/build
	../configure --target=$TARGET --prefix="$PREFIX" --disable-nls --enable-languages=c,c++ --without-headers
	make all-gcc
	make all-target-libgcc
	make install-gcc
	make install-target-libgcc
	cd ..
