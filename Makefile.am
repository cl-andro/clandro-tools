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

SUBDIRS = . scripts doc mirrors motds src

CONFFILES = \
etc/motd \
etc/motd.sh \
etc/motd-playstore \
etc/profile.d/init-clandro-properties.sh \
etc/clandro-login.sh

do_subst = sed -e "s%[@]CLANDRO_PREFIX[@]%$(clandro_prefix)%g" \
	       -e "s%[@]CLANDRO_APP_PACKAGE[@]%${clandro_app_package}%g" \
	       -e "s%[@]CLANDRO_BASE_DIR[@]%${clandro_base_dir}%g" \
	       -e "s%[@]CLANDRO_CACHE_DIR[@]%${clandro_cache_dir}%g" \
	       -e "s%[@]CLANDRO_HOME[@]%${clandro_android_home}%g" \
	       -e "s%[@]PACKAGE_VERSION[@]%${PACKAGE_VERSION}%g" \
	       -e "s%[@]CLANDRO_PACKAGE_FORMAT[@]%${CLANDRO_PACKAGE_FORMAT}%g" \
	       -e "s%[@]CLANDRO_PACKAGE_MANAGER[@]%${CLANDRO_PACKAGE_MANAGER}%g"

define sed-rule
$1: $1.in Makefile
	@echo "Creating $1"
	@$$(do_subst) < $(srcdir)/$1.in > $1
endef

# Login script
sysconf_DATA = clandro-login.sh

# profile.d script
pkgdata_PROFILE = init-clandro-properties.sh

pkgdata_EXAMPLES = clandro.properties

$(eval $(call sed-rule,init-clandro-properties.sh))

$(eval $(call sed-rule,clandro-login.sh))



create-deb-control-files:
	printf "" > conffiles
	for f in $(CONFFILES); do \
		printf "%s\n" "$$f" >> conffiles; \
	done
	printf "#!%s/bin/bash\n\n" "${clandro_prefix}" > preinst



install-data-local: create-deb-control-files $(pkgdata_PROFILE)
	$(MKDIR_P) $(DESTDIR)$(datarootdir)/examples/clandro
	for f in $(pkgdata_EXAMPLES); do \
		$(INSTALL) -m 644 $(srcdir)/$$f \
		$(DESTDIR)$(datarootdir)/examples/clandro; \
	done
	$(MKDIR_P) $(DESTDIR)$(sysconfdir)/profile.d
	for f in $(pkgdata_PROFILE); do \
		$(INSTALL) -m 644 $$f \
		$(DESTDIR)$(sysconfdir)/profile.d; \
	done

uninstall-local:
	for f in $(pkgdata_EXAMPLES); do \
		rm -f $(DESTDIR)$(datarootdir)/examples/clandro/$$f; \
	done
	-rmdir $(DESTDIR)$(datarootdir)/examples/clandro
	for f in $(pkgdata_PROFILE); do \
		rm -f $(DESTDIR)$(sysconfdir)/profile.d/$$f; \
	done
	-rmdir $(DESTDIR)$(sysconfdir)/profile.d

EXTRA_DIST = $(pkgdata_DATA) $(pkgdata_PROFILE) $(pkgdata_EXAMPLES)
