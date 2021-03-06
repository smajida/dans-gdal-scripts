# Copyright (c) 2013, Regents of the University of Alaska
# 
# All rights reserved.
# 
# Redistribution and use in source and binary forms, with or without modification, are permitted provided that the following conditions are met:
# 
#     * Redistributions of source code must retain the above copyright notice, this list of conditions and the following disclaimer.
#     * Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution.
#     * Neither the name of the Geographic Information Network of Alaska nor the names of its contributors may be used to endorse or promote products derived from this software without specific prior written permission.
# 
# THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
# "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
# LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR
# A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT OWNER OR
# CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL,
# EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
# PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR
# PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF
# LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING
# NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
# SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.




AC_PREREQ(2.37)
AC_INIT([dans-gdal-scripts], [0.24dev], [dan@stahlke.org])
AC_CONFIG_SRCDIR([src/common.h])
AC_CONFIG_HEADER([config.h])

AM_INIT_AUTOMAKE

AC_PROG_CXX
AC_LANG_CPLUSPLUS

# beginning of GDAL stuff #####################

AC_ARG_WITH(gdal,
[  --with-gdal=ARG  Include gdal support (ARG=path to gdal-config)],,)

if test "z$with_gdal" = "zyes" ; then
	AC_PATH_PROG([with_gdal], [gdal-config])
fi

if test "z$with_gdal" = "z"; then
	AC_PATH_PROG([with_gdal], [gdal-config])
fi

if test "z$with_gdal" = "zno" -o "z$with_gdal" = "z"; then
	AC_MSG_ERROR(gdal-config not found)
fi

GDALCONFIG=$with_gdal
AC_SUBST(GDALCFLAGS)
GDALCFLAGS=`${GDALCONFIG} --cflags`
AC_SUBST(GDALLIBS)
GDALLIBS=`${GDALCONFIG} --libs`

# Check for GDAL header files
SAVE_CPPFLAGS="${CPPFLAGS}"
CPPFLAGS="${CPPFLAGS} ${GDALCFLAGS}"
AC_CHECK_HEADERS([cpl_conv.h cpl_port.h cpl_string.h gdal.h ogr_api.h ogr_spatialref.h ogrsf_frmts.h], , \
				 [AC_MSG_ERROR([Could not find GDAL header files])])
CPPFLAGS="${SAVE_CPPFLAGS}"

# end of GDAL stuff #####################

# Replacements for functions not available in old autoconf versions.  These
# functions are needed by boost.m4.  Hopefully all systems should have working
# versions of sed and grep.
AC_DEFUN([AC_PROG_SED], [ SED="sed" AC_SUBST([SED]) ])
AC_DEFUN([AC_PROG_GREP], [ GREP="grep" AC_SUBST([GREP]) ])

# hopefully this is the right minimum version, I haven't really tested it
BOOST_REQUIRE([1.37])

# Checks for header files.
AC_HEADER_STDC

# Checks for typedefs, structures, and compiler characteristics.
AC_C_CONST
AC_HEADER_STDBOOL
AC_TYPE_SIZE_T

# Checks for library functions.
AC_FUNC_MALLOC
AC_FUNC_REALLOC
AC_FUNC_STRTOD
AC_CHECK_FUNCS([memset sqrt strtol])

AC_CHECK_LIB([m], [pow], , AC_MSG_ERROR([math library is required]))

AC_CONFIG_FILES([Makefile
                 src/Makefile])
AC_OUTPUT
