# Copyright (c) 2003-2006 Maksym Sobolyev
# Copyright (c) 2006-2008 Sippy Software, Inc.
# All rights reserved.
#
# Redistribution and use in source and binary forms, with or without
# modification, are permitted provided that the following conditions
# are met:
# 1. Redistributions of source code must retain the above copyright
#    notice, this list of conditions and the following disclaimer.
# 2. Redistributions in binary form must reproduce the above copyright
#    notice, this list of conditions and the following disclaimer in the
#    documentation and/or other materials provided with the distribution.
#
# THIS SOFTWARE IS PROVIDED BY THE AUTHOR AND CONTRIBUTORS ``AS IS'' AND
# ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
# IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE
# ARE DISCLAIMED.  IN NO EVENT SHALL THE AUTHOR OR CONTRIBUTORS BE LIABLE
# FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
# DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS
# OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION)
# HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT
# LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY
# OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF
# SUCH DAMAGE.
#
# $Id$

CC?=	gcc
CFLAGS+=-I../siplog -Wall -D_BSD_SOURCE -D_ISOC99_SOURCE
LIBS+=	-L../siplog -L/usr/local/lib -lsiplog -lpthread -lm
PREFIX?= /usr/local

OS = $(shell uname -s | sed -e s/SunOS/solaris/ -e s/CYGWIN.*/cygwin/ \
                 | tr "[A-Z]" "[a-z]")

ifeq ($(OS),solaris)
LIBS+=	-lsocket -lnsl -lxnet -lrt
endif

ifeq ($(OS),linux)
CFLAGS+= -D_BSD_SOURCE
endif

SRCS = main.c rtp_server.c rtpp_record.c rtpp_util.c rtp_resizer.c rtp.c rtpp_session.c \
  rtpp_command.c rtpp_network.c rtpp_log.c rtpp_notify.c
OBJS = $(SRCS:.c=.o)

.c.o:
	$(CC) -c $(CFLAGS) $< -o $@

all: rtpproxy

rtpproxy: $(OBJS)
	$(CC) -o rtpproxy $(OBJS) $(LIBS)

clean:
	rm -f rtpproxy $(OBJS)

install: all
	install rtpproxy $(PREFIX)/bin/rtpproxy