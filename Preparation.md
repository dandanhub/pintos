Pintos is a simple OS framework for 80x86 architecture.
The pintos project will run in a program that simulates an 80x86 CPU.

1. Getting Started
I will build Pintos on a Linux machine in particular a Ubuntu machine, ubuntu-16.04.2-desktop-amd64.

1.1 Install Pintos

1.1.1 Install Prerequisites
1) Required: GCC
sudo apt-get update
sudo apt-get install build-essential

/** 
build-essential will install the compiler and a bunch of related/needed packages:
dpkg-dev (>= 1.13.5) Debian package development tools
g++ (>= 4:4.4.3)GNU C++ compiler
gcc (>= 4:4.4.3) GNU C compiler
libc6-dev Embedded GNU C Library: Development Libraries and Header Files
or libc-dev virtual package provided by libc6-dev
make An utility for Directing compilation.
Reference: http://packages.ubuntu.com/trusty/build-essential
*/

2) Required: GNU Binutils
sudo apt-get install binutils

3) Required: Perl
sudo apt-get install perl

4) Required: GNU make
sudo apt-get install make

5) Recommended: QEMU
sudo apt-get install qemu-system

6) Recommended: GDB
sudo apt-get install gdb

7) Recommended: X
Skip

8) Optional: Texinfo
Skip

9) Optional: TEX
Skip

10) Optional: VMWare Player
Skip

1.1.2 Install Pintos
1) Install qemu
sudo apt-get install qemu

2) Install tcsh
2.1) Install tcsh using command:
sudo apt-get install tcsh
2.2) Edit .tcshrc file using command:
gedit .tcshrc
Put the text below into .tcshrc:
set path = (/home/dandanshi/pintos/src/utils $path)
2.3) Edit .bashrc.
Delete all old text and put the text below into .bashrc:
export PATH="/home/dandanshi/pintos/src/"

3) Untar pintos.tar.gz
tar -xf pintos.tar.gz

4) Edit pintos-gdb 
cd /home/dandanshi/pintos/src/utils
gedit pintos-gdb
change GDBMACROS = src/misc/gdb-macros to 
DBMACROS =/home/dandanshi/pintos/src/misc/gdb-macros

5) Edit Makefile
cd /home/dandanshi/pintos/src/utils
gedit Makefile
change “LDFLAGS = -lm” to:
“LDLIBS = -lm” 

6) make utils
cd /home/dandanshi/pintos/src/utils
make

7) edit Make.vars
cd /home/dandanshi/pintos/src/threads
gedit Make.vars
change SIMULATOR = --bochs to
SIMULATOR = --qemu

8) make threads 
cd /home/dandanshi/pintos/src/threads
make

9) Edit pintos
cd /home/dandanshi/pintos/src/utils
gedit pintos
Do the following change:
a) Ln 103: change $sim = "bochs" to 
$sim = "qemu"
b) Ln 259, change find_file('kernel.bin') to
find_file('/home/dandanshi/pintos/src/threads/build/kernel.bin')
c) Ln 623 change qemu to
qemu-system-x86_64

10) Edit Pintos.pm
cd /home/dandanshi/pintos/src/utils
gedit Pintos.pm
Do the following changes:
a) Ln 362: change 'loader.bin' to
'/home/dandanshi/pintos/src/threads/build/loader.bin'

1.2 Build Pintos
1) cd to thread folder
2）run the command:
sudo pintos run alarm-multiple

References:
Pintos IIITH (OS – PG), https://pintosiiith.wordpress.com/2012/09/13/install-pintos-with-qemu/
Installing PintOS on Ubuntu， https://www.youtube.com/watch?v=QdHOnsyPqso