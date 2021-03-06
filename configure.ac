dnl
dnl	Copyright (c) 2007-2012 Plecno s.r.l. All Rights Reserved 
dnl	info@plecno.com
dnl	via Giovio 8, 20144 Milano, Italy
dnl
dnl	Released under the terms of the GPLv3 or later
dnl
dnl	Author: Oreste Notelli <oreste.notelli@plecno.com>	
dnl

AC_PREREQ(2.68)
AC_COPYRIGHT(2007-2014 (c) Plecno s.r.l)
AC_INIT(justniffer, [0.5.13], info@plecno.com)
AC_DEFINE(JUSTNIFFER_VERSION, ["0.5.13"], [justniffer version])

AM_INIT_AUTOMAKE
AC_DEFINE([HAVE_LIB_PCAP], [], [has not libcap])
AM_CONFIG_HEADER(include/config.h)


AM_INIT_AUTOMAKE([-Wall -Werror])

dnl if test "$CXXFLAGS" = ""; then
dnl CXXFLAGS="-Os -Wall"
dnl fi

LIBNIDS="libnids-1.21_patched"
NIDS2_INCLUDE="-I ../lib/$LIBNIDS/src"
NIDS2_LIB="-L../lib/$LIBNIDS/src -lnids2"
PCAP_LIB="-lpcap"
AC_SUBST(NIDS2_INCLUDE)
AC_SUBST(NIDS2_LIB)
AC_SUBST(PCAP_LIB)

AC_CHECK_PROG(BASH_F, bash, "yes") 
echo "BASH_F= $BASH_F"
if test "$BASH_F" != "yes";
then
  AC_MSG_ERROR(["cannot find bash shell, download and build it: see www.gnu.org/software/bash/"])
fi
AC_CONFIG_MACRO_DIR([m4])
AC_PROG_CXX (gcc)
AC_PROG_CPP
AC_PROG_INSTALL
AC_CHECK_HEADERS([sys/time.h])
AC_C_CONST
AC_C_INLINE
AC_FUNC_STRFTIME
AC_HEADER_STDBOOL
AC_HEADER_TIME
AC_STRUCT_TM
AC_CHECK_HEADER(netinet/ip.h, , 
  AC_MSG_ERROR(["cannot find netinet/ip.h"]))
AC_PROG_LIBTOOL  
AC_CHECK_LIB(pcap, pcap_open_live, AC_DEFINE(HAVE_LIB_PCAP))

BOOST_REQUIRE([1.46])
 
BOOST_REGEX
BOOST_PROGRAM_OPTIONS
BOOST_IOSTREAMS

AC_CHECK_FILE(lib/$LIBNIDS/README.original, ,
[ AC_CHECK_PROG(PATCH, patch, yes, no) 
  if test "$PATCH" != yes;
  then
    AC_MSG_ERROR(["cannot find patch, download and build it: see http://www.gnu.org/software/patch/"])
  fi
  TAR_FOUND=""
  AC_CHECK_PROG(TAR, tar, yes) 
  if test "$TAR" != yes;
  then
    AC_MSG_ERROR(["cannot find tar"])
  fi
  AC_CHECK_FILE(lib/$LIBNIDS/src/nids2.h, , AC_MSG_ERROR(["cannot find patched libnids"]))
  ]
)

AC_CONFIG_SUBDIRS([lib/libnids-1.21_patched])
AX_PYTHON

PYTHONCODEDIR=${datarootdir}/justniffer/scripts
AC_SUBST(PYTHONCODEDIR)
if test "$ax_python_bin" != "no"; then
  PYTHONSUBDIR="python"
fi

if test "$ax_python_header" != "no"; then
  PYTHON_MODULES="python.cpp"
fi


AC_SUBST(PYTHONSUBDIR)

	
AC_OUTPUT(Makefile src/Makefile python/Makefile )
