AC_INIT([rtmpdump], [2.4], [])
AC_CONFIG_MACRO_DIR([m4])
AM_INIT_AUTOMAKE([foreign -Wall -Wno-extra-portability -Werror])
LT_INIT
AC_PROG_CC

#### Find OpenSSL
AC_MSG_CHECKING([for --with-openssl])
AC_ARG_WITH(
            [openssl],
            [AS_HELP_STRING([--with-openssl],[/absolute/path/to/openssl-base])],
            [ LDFLAGS="$LDFLAGS -L$with_openssl/lib";
              CFLAGS="$CFLAGS -I$with_openssl/include/";
              LIBS="-lssl";
              AC_MSG_RESULT([$with_openssl])
              ],
            [AC_MSG_RESULT([no])]
            )

AC_CHECK_LIB([crypto],[CRYPTO_new_ex_data], [], [AC_MSG_ERROR([OpenSSL libraries required])])
AC_CHECK_LIB([ssl],[SSL_library_init], [], [AC_MSG_ERROR([OpenSSL libraries required])])
AC_CHECK_HEADERS([openssl/crypto.h openssl/x509.h openssl/pem.h openssl/ssl.h openssl/err.h],[],[AC_MSG_ERROR([OpenSSL headers required])])

AC_CHECK_LIB([pthread], [pthread_create], [], [AC_MSG_ERROR([pthread library required])])

AC_CONFIG_HEADERS([config.h])
AC_CONFIG_FILES([Makefile librtmp/Makefile src/Makefile])
AC_OUTPUT
