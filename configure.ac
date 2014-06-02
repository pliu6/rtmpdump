#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ([2.68])
AC_INIT([rtmpdump], [2.4], [])
AM_INIT_AUTOMAKE([foreign -Wall -Werror])
AM_PROG_AR
LT_PREREQ([2.2])
LT_INIT([dlopen])
AC_CONFIG_MACRO_DIR([m4])
AC_CONFIG_SRCDIR([config.h.in])
AC_CONFIG_HEADERS([config.h])

# Checks for programs.
AC_PROG_CXX
AC_PROG_AWK
AC_PROG_CC
AC_PROG_CPP
AC_PROG_INSTALL
AC_PROG_LN_S
AC_PROG_MAKE_SET

AC_CHECK_LIB([pthread], [pthread_create], [], [AC_MSG_ERROR([pthread library required])])

AC_ARG_WITH([crypto],
            AS_HELP_STRING([--with-crypto],[Use crypto (openssl, gnutls, polarssl, none)]),
            [ac_cv_crypto="$withval"], [ac_cv_crypto="openssl"])

AC_MSG_NOTICE([Using $ac_cv_crypto as crypto])
case "${ac_cv_crypto}" in
  openssl)
    AC_DEFINE(USE_OPENSSL, 1, [Use openssl])
    AC_CHECK_LIB([ssl],[SSL_library_init], [], [AC_MSG_ERROR([OpenSSL libraries required])])
    AC_CHECK_LIB([crypto],[CRYPTO_new_ex_data], [], [AC_MSG_ERROR([OpenSSL libraries required])])
    AC_CHECK_LIB([z], [gzopen], [], [AC_MSG_ERROR([zlib required])])
    AC_SUBST(RTMP_DEPENDENCIES, ["libssl,libcrypto,libz"])
    ;;
  gnutls)
    AC_DEFINE(USE_GNUTLS, 1, [Use gnutls])
    AC_CHECK_LIB([gnutls], [gnutls_init], [], [AC_MSG_ERROR([GnuTLS libraries required])])
    AC_CHECK_LIB([nettle], [nettle_MD5Init], [], [AC_MSG_ERROR([nettle libraries required])], [-lhogweed])
    AC_CHECK_LIB([gmp], [__gmpz_init], [], [AC_MSG_ERROR([gmp libraries required])])
    AC_CHECK_LIB([z], [gzopen], [], [AC_MSG_ERROR([zlib required])])
    AC_SUBST(RTMP_DEPENDENCIES, ["libgnutls,libnettle,libgmp,libz"])
    ;;
  polarssl)
    AC_DEFINE(USE_POLARSSL, 1, [Use polarssl])
    AC_CHECK_LIB([polarssl], [havege_init], [], [AC_MSG_ERROR([polarssl libraries required])])
    AC_CHECK_LIB([z], [gzopen], [], [AC_MSG_ERROR([zlib required])])
    AC_SUBST(RTMP_DEPENDENCIES, ["libpolarssl,libz"])
    ;;
  none|*)
    AC_MSG_WARN([turn off all crypto support, you must specify one of --with-crypto={openssl, gnutls, polarssl} if you would like to build with crypto])
    AC_DEFINE(NO_CRYPTO, 1, [No crypto])
    ;;
esac

AC_ARG_ENABLE([ssl],
              AS_HELP_STRING([--disable-ssl],[disable ssl]))

AS_IF([test "x$enable_ssl" = "xno"],
      [AC_DEFINE([NO_SSL], [1], [Define to disable SSL])])

# Checks for header files.
AC_CHECK_HEADERS([arpa/inet.h fcntl.h limits.h netdb.h netinet/in.h stddef.h stdint.h stdlib.h string.h sys/param.h sys/socket.h unistd.h])
# Checks for typedefs, structures, and compiler characteristics.
AC_C_INLINE
AC_TYPE_INT16_T
AC_TYPE_INT32_T
AC_TYPE_INT8_T
AC_TYPE_OFF_T
AC_TYPE_SIZE_T
AC_HEADER_STDBOOL
AC_TYPE_UINT32_T
AC_TYPE_UINT8_T

# Checks for library functions.
AC_FUNC_FORK
AC_FUNC_FSEEKO
AC_FUNC_MALLOC
AC_FUNC_MKTIME
AC_FUNC_REALLOC
AC_FUNC_STRTOD
AC_CHECK_FUNCS([gethostbyname inet_ntoa memchr memset select socket strcasecmp strchr strdup strerror strncasecmp strrchr strstr strtol])

AC_CONFIG_FILES([Makefile
                 librtmp/Makefile
                 librtmp/librtmp.pc
                 src/Makefile])
AC_OUTPUT
