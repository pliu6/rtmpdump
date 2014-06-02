lib_LTLIBRARIES = librtmp.la
librtmpincludedir = $(includedir)/librtmp
librtmpinclude_HEADERS = rtmp.h rtmp_sys.h log.h amf.h
librtmp_la_SOURCES = rtmp.c log.c amf.c hashswf.c parseurl.c bytes.h dhgroups.h dh.h handshake.h http.h

librtmp_la_LDFLAGS = -version-info 2:4:0

pkgconfiglibdir = $(libdir)/pkgconfig
pkgconfiglib_DATA = librtmp.pc
