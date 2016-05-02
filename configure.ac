m4_define([version_current], [1])
m4_define([version_revision], [0])
m4_define([version_age], [0])

AC_INIT([libmmap], [version_current.version_revision.version_age])

AC_CONFIG_HEADERS([mmap/config.h])
AC_CONFIG_SRCDIR([./])

AC_CONFIG_AUX_DIR([build/autoconf])
AC_CONFIG_MACRO_DIR([build/autoconf])
AM_INIT_AUTOMAKE([subdir-objects])

LIBMMAP_VERSION=version_current:version_revision:version_age
AC_SUBST(LIBMMAP_VERSION)

AM_PROG_AR
AC_PROG_LIBTOOL
AC_PROG_CC_C99

AS_IF([test "$ac_cv_prog_cc_c99" = "no"], AC_MSG_ERROR([C99 support is required but not found.]))

AC_ARG_ENABLE(debug,        [  --enable-debug          Enable assert() statements for debugging.], [enable_debug=yes])

# Debugging support
if test "x$enable_debug" = x"yes"; then
   DEBUG_FLAGS="-g"
   AC_SUBST(DEBUG_FLAGS)
else
   AC_DEFINE(NDEBUG,1,[Define whether debugging is enabled])
fi

AX_VALGRIND_CHECK()

AC_SEARCH_LIBS(aes_randinit,aesrand)
if test "x$ac_cv_search_aes_randinit" = "xno"; then
   AC_MSG_ERROR([libaesrand not found])
fi
AC_SEARCH_LIBS(clt_state_init,clt13)
if test "x$ac_cv_search_clt_state_init" = "xno"; then
   AC_MSG_ERROR([libclt13 not found])
fi
AC_SEARCH_LIBS(fmpz_init,flint)
if test "x$ac_cv_search_fmpz_init" = "xno"; then
   AC_MSG_ERROR([libflint not found])
fi

AC_CONFIG_FILES([Makefile mmap/Makefile tests/Makefile])

AC_OUTPUT