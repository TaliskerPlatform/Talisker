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

AC_CANONICAL_BUILD
AC_CANONICAL_HOST
AC_CANONICAL_TARGET
AC_CANONICAL_SYSTEM

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

freestanding_subdirs=''
TAL_CONFIG_SUBDIR([Frameworks/PersonalityKit/ISOC],[Freestanding/ISOC],,[freestanding_subdirs="$freestanding_subdirs ISOC"])
TAL_CONFIG_SUBDIR([Applications/SystemStartup],[Freestanding/SystemStartup],,[freestanding_subdirs="$freestanding_subdirs SystemStartup"])
AC_SUBST([freestanding_subdirs])

## Native components are built next: these are also built for the HOST system,
## but without any runtime support — any kernel calls made by native components
## must be made directly, because there is no C Library to to perform them.

native_subdirs=''
TAL_CONFIG_SUBDIR([Frameworks/PersonalityKit],[Native/PersonalityKit],,[native_subdirs="$native_subdirs PersonalityKit"])
TAL_CONFIG_SUBDIR([Applications/SystemStartup],[Native/SystemStartup],,[native_subdirs="$native_subdirs SystemStartup"])
AC_SUBST([native_subdirs])

## Finally, build the hosted components: the components which are compiled
## for the host system

hosted_subdirs=''
TAL_CONFIG_SUBDIR([Frameworks],[Hosted/Frameworks],,[hosted_subdirs="$hosted_subdirs Frameworks"])
TAL_CONFIG_SUBDIR([Developer],[Hosted/Developer],,[hosted_subdirs="$hosted_subdirs Developer"])
TAL_CONFIG_SUBDIR([Applications/SystemStartup],[Hosted/SystemStartup],,[hosted_subdirs="$hosted_subdirs SystemStartup"])
AC_SUBST([hosted_subdirs])

dnl This can go away once there's a standalone Documentation project
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
