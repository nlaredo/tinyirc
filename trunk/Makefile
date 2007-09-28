# tinyirc makefile
# by Nathan Laredo
#
# I don't wish to assert any rights (copyright) over this makefile
# but please give me credit if you use my code.

# Comment the following line to disable ctcp support
CTCP		= -DDO_CTCP

DESTDIR		=
prefix		= /usr
exec_prefix	= $(prefix)
man_prefix	= $(prefix)/share

INSTALL		= /usr/bin/install
INSTALL_BIN	= $(INSTALL) -m 755
INSTALL_DATA	= $(INSTALL) -m 644
INSTALL_OBJS	= tinyirc

MANDIR		= $(DESTDIR)$(man_prefix)/man/man1
BINDIR		= $(DESTDIR)$(exec_prefix)/bin

INCLUDES	= -I/usr/include/ncurses 

SERVER = irc.freenode.org
PORT = 6667
#
all: help gnu

help:
	## Please use "make target"
	## where target is one of the following
	##
	## aix	  hpux	  gnu	 posix	  generic    debug
	##
	## If you have trouble with the input line, try a different target

debug:
	$(MAKE) tinyirc CFLAGS=-g LDFLAGS=-g CC=gcc LIBS=-ltermcap

generic:
	$(MAKE) tinyirc CFLAGS=-O LDFLAGS=-s LIBS=-ltermcap

aix:
	$(MAKE) tinyirccv CFLAGS="-O -D_AIX_" \
		LDFLAGS=-s LIBS=-lcurses CC=bsdcc

posix:
	$(MAKE) tinyirc CFLAGS="-O2 -m486 -DPOSIX" LDFLAGS="-s" LIBS=-ltermcap

gnu:
	$(MAKE) tinyirc CFLAGS="-g -O2 -pipe -DPOSIX -Wall -Wunused -Wformat" \
		LDFLAGS= LIBS=-ltermcap CC=gcc

hpux:
	$(MAKE) tinyirccv LDFLAGS=-s LIBS=-lcurses

ntest:
	$(MAKE) tinyirccv CFLAGS="-O -I/usr/include/ncurses -DPOSIX" \
		LDFLAGS="-L/usr/local/lib" LIBS=-lncurses CC=gcc

ctest:
	$(MAKE) tinyirccv CFLAGS=-O LDFLAGS=-s LIBS=-lcurses

DEFINES = -DDEFAULTSERVER=\"$(SERVER)\" -DDEFAULTPORT=$(PORT) $(CTCP) $(INCLUDES)

tinyirc: tinyirc.o
	$(CC) $(LDFLAGS) -o tinyirc tinyirc.o $(LIBS)

tinyirccv: tinyirccv.o
	$(CC) $(LDFLAGS) -o tinyirc tinyirccv.o $(LIBS)

tinyirc.o: tinyirc.c Makefile
	$(CC) $(CFLAGS) $(DEFINES) -c tinyirc.c -o tinyirc.o

tinyirccv.o: tinyirccv.c Makefile
	$(CC) $(CFLAGS) $(DEFINES) -c tinyirccv.c -o tinyirccv.o

clean:
	-rm -f *.o *.exe *[~#]

install-bin:
	$(INSTALL_BIN) -d $(BINDIR)
	$(INSTALL_BIN) -s $(INSTALL_OBJS) $(BINDIR)

install-man:
	$(INSTALL_BIN) -d $(MANDIR)
	$(INSTALL_DATA) *.1 $(MANDIR)

install: all install-bin

#EOF
