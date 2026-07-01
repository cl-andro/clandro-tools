dnl  Autoconf script for clandro-tools
dnl To rebuild the 'configure' script from this, execute the command
dnl	autoconf
dnl in the directory containing this script.
dnl
dnl Copyright (C) 2022-2025 Clandro
dnl
dnl  This file is part of clandro-tools.
dnl
dnl  clandro-tools is free software: you can redistribute it
dnl  and/or modify it under the terms of the GNU General Public
dnl  License as published by the Free Software Foundation, either
dnl  version 3 of the License, or (at your option) any later version.
dnl
dnl  clandro-tools is distributed in the hope that it will be
dnl  useful, but WITHOUT ANY WARRANTY; without even the implied
dnl  warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
dnl  See the GNU General Public License for more details.
dnl
dnl  You should have received a copy of the GNU General Public License
dnl  along with clandro-tools.  If not, see
dnl  <https://www.gnu.org/licenses/>.

AC_PREREQ([2.69])
AC_INIT([clandro-tools], [1.48.0], [support@clandro.dev])

AM_INIT_AUTOMAKE([foreign])

AC_PROG_MAKE_SET
AC_PROG_CC
AC_LANG(C)

copyright="Copyright (C) 2022-2025 Clandro."
if test "${CLANDRO_APP_PACKAGE+set}" = set; then
  clandro_app_package="$CLANDRO_APP_PACKAGE"
else
  clandro_app_package="com.clandro"
fi
if test "${CLANDRO_BASE_DIR+set}" = set; then
  clandro_base_dir="$CLANDRO_BASE_DIR"
else
  clandro_base_dir="/data/data/$clandro_app_package/files"
fi
if test "${CLANDRO_CACHE_DIR+set}" = set; then
  clandro_cache_dir="$CLANDRO_CACHE_DIR"
else
  clandro_cache_dir="/data/data/$clandro_app_package/cache"
fi
if test "${CLANDRO_PREFIX+set}" = set; then
  clandro_prefix="$CLANDRO_PREFIX"
else
  clandro_prefix="$clandro_base_dir/usr"
fi
if test "${CLANDRO_ANDROID_HOME+set}" = set; then
  clandro_android_home="$CLANDRO_ANDROID_HOME"
else
  clandro_android_home="$clandro_base_dir/home"
fi
if test "${CLANDRO_PACKAGE_FORMAT+set}" = set; then
  clandro_package_format="$CLANDRO_PACKAGE_FORMAT"
else
  clandro_package_format="debian"
fi
if test "${CLANDRO_PACKAGE_MANAGER+set}" = set; then
  clandro_package_manager="$CLANDRO_PACKAGE_MANAGER"
else
  clandro_package_manager="apt"
fi

AC_DEFINE_UNQUOTED(COPYRIGHT, ["$copyright"],
  [Short copyright string for this version of clandro-tools.])
AC_DEFINE_UNQUOTED(CLANDRO_APP_PACKAGE, ["$clandro_app_package"],
  [Clandro namespace])
AC_DEFINE_UNQUOTED(CLANDRO_BASE_DIR, ["$clandro_base_dir"],
  [Base directory of clandro application])
AC_DEFINE_UNQUOTED(CLANDRO_CACHE_DIR, ["$clandro_cache_dir"],
  [Cache directory of clandro application])
AC_DEFINE_UNQUOTED(CLANDRO_PREFIX, ["$clandro_prefix"],
  [Clandro prefix])
AC_DEFINE_UNQUOTED(CLANDRO_ANDROID_HOME, ["$clandro_android_home"],
  [Clandro home directory])
AC_DEFINE_UNQUOTED(CLANDRO_PACKAGE_FORMAT, ["$clandro_package_format"],
  [Packaging format (debian or pacman)])
AC_DEFINE_UNQUOTED(CLANDRO_PACKAGE_MANAGER, ["$clandro_package_manager"],
  [Package manager (apt or pacman)])

AC_SUBST(clandro_app_package)
AC_SUBST(clandro_base_dir)
AC_SUBST(clandro_cache_dir)
AC_SUBST(clandro_prefix)
AC_SUBST(clandro_android_home)
AC_SUBST(clandro_package_format)
AC_SUBST(clandro_package_manager)

AC_PROG_LN_S

AC_CONFIG_FILES([Makefile scripts/Makefile doc/Makefile
mirrors/Makefile motds/Makefile src/Makefile])

AC_OUTPUT
