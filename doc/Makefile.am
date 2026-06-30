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

man_MANS = clandro.1

clandro.1.md: ${srcdir}/clandro.1.md.in
	@echo "Creating clandro.1.md"
	@sed -e "s%[@]CLANDRO_PREFIX[@]%$(clandro_prefix)%g" \
	    -e "s%[@]CLANDRO_HOME[@]%${clandro_android_home}%g" \
	${srcdir}/clandro.1.md.in > clandro.1.md

clandro.1: clandro.1.md
	@echo "Generating clandro.1"
	@pandoc --standalone --to man --output clandro.1 clandro.1.md
