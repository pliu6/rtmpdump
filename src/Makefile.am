LDADD = ../librtmp/librtmp.la
AM_CPPFLAGS = -I$(srcdir)/../librtmp -DRTMPDUMP_VERSION=\"$(VERSION)\"
bin_PROGRAMS = rtmpdump rtmpgw rtmpsrv rtmpsuck
rtmpdump_SOURCES = rtmpdump.c
rtmpgw_SOURCES = rtmpgw.c thread.c thread.h
rtmpsrv_SOURCES = rtmpsrv.c thread.c thread.h
rtmpsuck_SOURCES = rtmpsuck.c thread.c thread.h
