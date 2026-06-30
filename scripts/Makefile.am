# Copyright (C) 2022 Clandro

# This file is part of clandro-tools.

# clandro-tools is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.

# clandro-tools is distributed in the hope that it will be useful, but
# WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
# General Public License for more details.

# You should have received a copy of the GNU General Public License
# along with clandro-tools.  If not, see
# <https://www.gnu.org/licenses/>.

# shell scripts:
bin_SCRIPTS = chsh dalvikvm login pkg su clandro-backup			\
clandro-change-repo clandro-fix-shebang clandro-info clandro-open		\
clandro-open-url clandro-reload-settings clandro-reset clandro-restore	\
clandro-setup-package-manager clandro-setup-storage clandro-wake-lock	\
clandro-wake-unlock

# wrappers around tools in /system/bin:
bin_SCRIPTS += df getprop logcat ping ping6 pm settings top

CLEANFILES = $(bin_SCRIPTS)

do_subst = sed -e "s%[@]CLANDRO_PREFIX[@]%$(clandro_prefix)%g" \
	       -e "s%[@]CLANDRO_APP_PACKAGE[@]%${clandro_app_package}%g" \
	       -e "s%[@]CLANDRO_BASE_DIR[@]%${clandro_base_dir}%g" \
	       -e "s%[@]CLANDRO_CACHE_DIR[@]%${clandro_cache_dir}%g" \
	       -e "s%[@]CLANDRO_HOME[@]%${clandro_android_home}%g" \
	       -e "s%[@]PACKAGE_VERSION[@]%${PACKAGE_VERSION}%g" \
	       -e "s%[@]CLANDRO_PACKAGE_FORMAT[@]%${clandro_package_format}%g" \
	       -e "s%[@]CLANDRO_PACKAGE_MANAGER[@]%${clandro_package_manager}%g"

define tool-rule
$1: $1.in Makefile
	@echo "Creating $1"
	@$$(do_subst) < $(srcdir)/$1.in > $1
	@chmod u+x $1
endef

define wrapper-rule
$1: Makefile
	@echo "Creating $1 wrapper"
	@echo '#!/bin/sh' > $1
# Remove LD_LIBRARY_PATH from environment to avoid conflicting
# with system libraries that system binaries may link against
	@echo 'unset LD_LIBRARY_PATH LD_PRELOAD' >> $1
# Some tools require having /system/bin/app_process in the PATH,
# at least am&pm on a Nexus 6p running Android 6.0
	@echo -n 'PATH=/system/bin ' >> $1
	@echo "exec /system/bin/$1 \"\$$$$@\"" >> $1
	@chmod u+x $1
endef

install-exec-hook:
	@$(LN_S) -f clandro-open $(DESTDIR)$(bindir)/xdg-open

$(eval $(call tool-rule,chsh))
$(eval $(call tool-rule,dalvikvm))
$(eval $(call tool-rule,login))
$(eval $(call tool-rule,pkg))
$(eval $(call tool-rule,su))
$(eval $(call tool-rule,clandro-backup))
$(eval $(call tool-rule,clandro-change-repo))
$(eval $(call tool-rule,clandro-fix-shebang))
$(eval $(call tool-rule,clandro-info))
$(eval $(call tool-rule,clandro-open))
$(eval $(call tool-rule,clandro-open-url))
$(eval $(call tool-rule,clandro-reload-settings))
$(eval $(call tool-rule,clandro-reset))
$(eval $(call tool-rule,clandro-restore))
$(eval $(call tool-rule,clandro-setup-package-manager))
$(eval $(call tool-rule,clandro-setup-storage))
$(eval $(call tool-rule,clandro-wake-lock))
$(eval $(call tool-rule,clandro-wake-unlock))

$(eval $(call wrapper-rule,df))
$(eval $(call wrapper-rule,getprop))
$(eval $(call wrapper-rule,logcat))
$(eval $(call wrapper-rule,mount))
$(eval $(call wrapper-rule,ping))
$(eval $(call wrapper-rule,ping6))
$(eval $(call wrapper-rule,pm))
$(eval $(call wrapper-rule,settings))
$(eval $(call wrapper-rule,top))
$(eval $(call wrapper-rule,umount))
