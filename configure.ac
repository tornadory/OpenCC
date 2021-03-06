#
# Open Chinese Convert
#
# Copyright 2010 BYVoid <byvoid1@gmail.com>
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#

m4_define([package_name], [opencc])
m4_define([opencc_released], [1])
m4_define([opencc_major_version], [0])
m4_define([opencc_minor_version], [1])
m4_define([opencc_micro_version], [1])
m4_define(opencc_maybe_datestamp,
	m4_esyscmd([if test x]opencc_released[ != x1; then date +.%Y%m%d | tr -d '\n\r'; fi]))

m4_define([opencc_version],
	opencc_major_version.opencc_minor_version.opencc_micro_version[]opencc_maybe_datestamp)

m4_define([package_url], [http://code.google.com/p/open-chinese-convert])
m4_define([package_url_bugreport], [http://code.google.com/p/open-chinese-convert/issues/entry])

AC_INIT([package_name], [opencc_version], [package_url_bugreport], [package_name], [package_url])
AC_CANONICAL_HOST

AM_INIT_AUTOMAKE([1.10])
AC_GNU_SOURCE

AC_CONFIG_HEADERS([config.h])
AC_CONFIG_MACRO_DIR([m4])
m4_ifdef([AM_SILENT_RULES],[AM_SILENT_RULES([yes])])

AS_VERSION
AS_NANO
AM_SANITY_CHECK
AM_MAINTAINER_MODE
AM_DISABLE_STATIC
AC_PROG_CC
AM_PROG_CC_C_O
AC_PROG_RANLIB
AC_ISC_POSIX
AC_HEADER_STDC
AM_PROG_LIBTOOL

AC_C_BIGENDIAN
if test "x$ac_cv_c_bigendian" = "xyes"; then
	BYTEORDER="BIG_ENDIAN"
else
	BYTEORDER="LITTLE_ENDIAN"
fi
AC_SUBST(BYTEORDER)

case "${host}" in
	*-apple-*) LIB_ICONV="-liconv" ;;
	*)	LIB_ICONV="" ;;
esac
AC_SUBST(LIB_ICONV)

# If only source code changed, lt_revision + 1
# If any interface added, lt_age + 1
# If any interfaces changed or removed, lt_current + 1, lt_revision = 0, lt_age = 0
m4_define([lt_current], [1])
m4_define([lt_revision], [0])
m4_define([lt_age], [0])
LT_VERSION_INFO="lt_current:lt_revision:lt_age"
AC_SUBST(LT_VERSION_INFO)

AC_CHECK_HEADERS([sys/mman.h])

# define GETTEXT
AM_GNU_GETTEXT([external])
AM_GNU_GETTEXT_VERSION(0.16.1)

# OUTPUT files
AC_CONFIG_FILES([po/Makefile.in
Makefile
opencc.pc
opencc.spec
data/Makefile
doc/Makefile
m4/Makefile
src/Makefile
test/Makefile
])

AC_OUTPUT

AC_MSG_RESULT([
Open Chinese Convert (OpenCC)
    Version                     $VERSION
    Library Version             libopencc.lt_current.lt_revision.lt_age

Build options:
    C Build Flags               $CFLAGS
    Install prefix              $prefix
])
