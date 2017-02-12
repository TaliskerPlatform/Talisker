## Talisker Platform

## Copyright 2017 Mo McRoberts.
##
##  Licensed under the Apache License, Version 2.0 (the "License");
##  you may not use this file except in compliance with the License.
##  You may obtain a copy of the License at
##
##      http://www.apache.org/licenses/LICENSE-2.0
##
##  Unless required by applicable law or agreed to in writing, software
##  distributed under the License is distributed on an "AS IS" BASIS,
##  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
##  See the License for the specific language governing permissions and
##  limitations under the License.

AC_INIT([Talisker],[develop])

AC_CONFIG_AUX_DIR([Developer/Library/BuildScripts])
AC_CONFIG_MACRO_DIR([Developer/Library/M4])

TAL_CANONICAL_SYSTEM

AM_INIT_AUTOMAKE([foreign])
AM_MAINTAINER_MODE

## Determine default domain paths
TAL_CHECK_DOMAINS

## Configure components for the BUILD system first (i.e., the system
## that this configure script is being executed on).
##
## These components are configured and built in the 'Build' subdirectory;
## executables are built for the system this script is being executed on,
## but produce output suitable for the HOST system (i.e., the system Talisker
## will run on).
##
## Thus, these components are configured with:-
##   --build=$build
##   --host=$build
##   --target=$host

build_subdirs=''
TAL_CONFIG_SUBDIR([Developer],[Build/Developer],,[build_subdirs="$build_subdirs Developer"],[$build],[$host],[$build])
AC_SUBST([build_subdirs])

## Next, components which should be built for a freestanding environment -
## that is, the HOST system (the system that executables are compiled for),
## but without an operating system of any sort.
##
## XXX: building certain freestanding components (e.g., a kernel) should make
## it possible to build native components when it otherwise wouldn't be.
AC_MSG_CHECKING([whether freestanding components should be built])
AC_ARG_ENABLE([freestanding],[AS_HELP_STRING([--disable-freestanding],[do not build freestanding components (default=auto)])],[should_build_freestanding=$enableval],[should_build_freestanding=auto])
freestanding_subdirs=''
if test x"$should_build_freestanding" = x"no" ; then
	AC_MSG_RESULT([no])
elif test x"$host_variant_freestanding" = x"" ; then
	AC_MSG_RESULT([no])
	if test x"$should_build_freestanding" = x"yes" ; then
		AC_MSG_ERROR([--enable-freestanding was supplied but the freestanding variant of ${host} could not be determined])
	fi
else
	AC_MSG_RESULT([yes (for $host_variant_freestanding)])
	TAL_CONFIG_SUBDIR([Frameworks/PersonalityKit/ISOC],[Freestanding/ISOC],,[freestanding_subdirs="$freestanding_subdirs ISOC"],[$host_variant_freestanding],[$host_variant_freestanding])
	TAL_CONFIG_SUBDIR([Applications/SystemStartup],[Freestanding/SystemStartup],,[freestanding_subdirs="$freestanding_subdirs SystemStartup"],[$host_variant_freestanding],[$host_variant_freestanding])
fi
AC_SUBST([freestanding_subdirs])

## Native components are built next: these are also built for the HOST system,
## but without any runtime support — any kernel calls made by native components
## must be made directly, because there is no C Library to to perform them.
##
## XXX building certain native components (e.g., a libc) should make it
## possible 
AC_MSG_CHECKING([whether native components should be built])
AC_ARG_ENABLE([native],[AS_HELP_STRING([--disable-native],[do not build native components (default=auto)])],[should_build_native=$enableval],[should_build_native=auto])

native_subdirs=''
if test x"$should_build_native" = x"no" ; then
	AC_MSG_RESULT([no])
elif test x"$host_variant_native" = x"" ; then
	AC_MSG_RESULT([no])
	if test x"$should_build_native" = x"yes" ; then
		AC_MSG_ERROR([--enable-native was supplied but the native variant of ${host} could not be determined])
	fi
else
	AC_MSG_RESULT([yes (for $host_variant_native)])
	TAL_CONFIG_SUBDIR([Frameworks/PersonalityKit],[Native/PersonalityKit],,[native_subdirs="$native_subdirs PersonalityKit"],[$host_variant_native],[$host_variant_native])
	TAL_CONFIG_SUBDIR([Applications/SystemStartup],[Native/SystemStartup],,[native_subdirs="$native_subdirs SystemStartup"],[$host_variant_native],[$host_variant_native])
fi
AC_SUBST([native_subdirs])

## Finally, build the hosted components: the components which are compiled
## for the host system

AC_MSG_CHECKING([whether hosted components should be built])
AC_ARG_ENABLE([hosted],[AS_HELP_STRING([--disable-hosted],[do not build hosted components (default=auto)])],[should_build_hosted=$enableval],[should_build_hosted=auto])
hosted_subdirs=''
if test x"$should_build_hosted" = x"no" ; then
	AC_MSG_RESULT([no])
elif test x"$host_variant_hosted" = x"" ; then
	AC_MSG_RESULT([no])
	if test x"$should_build_hosted" = x"yes" ; then
		AC_MSG_ERROR([--enable-hosted was supplied but the hosted variant of ${host} could not be determined])
	fi
else
	AC_MSG_RESULT([yes (for $host_variant_hosted)])
	TAL_CONFIG_SUBDIR([Frameworks],[Hosted/Frameworks],,[hosted_subdirs="$hosted_subdirs Frameworks"],[$host_variant_hosted],[$host_variant_hosted])
	TAL_CONFIG_SUBDIR([Developer],[Hosted/Developer],,[hosted_subdirs="$hosted_subdirs Developer"],[$host_variant_hosted],[$host_variant_hosted])
# Note: it will be important to skip SystemStartup when recursing into
# the Applications dir, because configuring it in-place may break future
# configure runs (i.e., if $srcdir=$builddir)
	TAL_CONFIG_SUBDIR([Applications/SystemStartup],[Hosted/SystemStartup],,[hosted_subdirs="$hosted_subdirs SystemStartup"],[$host_variant_hosted],[$host_variant_hosted])
	TAL_CONFIG_SUBDIR([Personalities],,,[subdirs="$subdirs Personalities"],[$host_variant_hosted],[$host_variant_hosted])
fi
AC_SUBST([hosted_subdirs])

dnl This can go away once Documentation is a stand-alone project
docs_subdirs=''
TAL_CONFIG_SUBDIR([Documentation/UserGuide],,,[docs_subdirs="$docs_subdirs UserGuide"])
AC_SUBST([docs_subdirs])

top_subdirs=''
TAL_CONFIG_SUBDIR([Library],,,[top_subdirs="$top_subdirs Library"])
TAL_CONFIG_SUBDIR([Personalities],,,[top_subdirs="$top_subdirs Personalities"])
top_subdirs="$top_subdirs Applications Documentation"
AC_SUBST([top_subdirs])

AC_CONFIG_FILES([
Makefile
Build/Makefile
Freestanding/Makefile
Native/Makefile
Hosted/Makefile
Documentation/Makefile
Applications/Makefile
])

AC_OUTPUT
