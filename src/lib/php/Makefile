######################################################################
# Copyright (C) 2011-2012 Hewlett-Packard Development Company, L.P.
#
# This library is free software; you can redistribute it and/or
# modify it under the terms of the GNU Lesser General Public
# License version 2.1 as published by the Free Software Foundation.
#
# This library is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
# Lesser General Public License for more details.
#
# You should have received a copy of the GNU Lesser General Public License
# along with this library; if not, write to the Free Software Foundation, Inc.0
# 51 Franklin Street, Fifth Floor, Boston, MA  02110-1301  USA
######################################################################

TOP = ../../..
VARS = $(TOP)/Makefile.conf
include $(VARS)

FILES = `find . -type f | grep -v svn |grep -v tests | grep -E "(php)$$"`

all: bootstrap services.xml

# generate the postinstall script
bootstrap: bootstrap-process_php

# generate service.xml
services.xml: services.xml-process

# include the preprocessing stuff
include $(TOP)/Makefile.process

install: all
	mkdir -p $(DESTDIR)$(MODDIR)/lib/php
	for file in $(FILES); do \
		$(INSTALL_DATA) $$file $(DESTDIR)$(MODDIR)/lib/php/$$file; \
	done
	$(INSTALL_DATA) services.xml $(DESTDIR)$(MODDIR)/lib/php/services.xml

uninstall:
	@echo "Removing php libs"
	rm -rf $(DESTDIR)$(MODDIR)/lib/php

clean:
	rm -f *.o core bootstrap.php services.xml

test:
	$(MAKE) -C tests test

coverage:
	$(MAKE) -C tests coverage

.PHONY: all install uninstall clean test
