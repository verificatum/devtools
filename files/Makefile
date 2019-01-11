
# Copyright 2008-2018 Douglas Wikstrom
#
# This file is part of Verificatum Mix-Net (VMN).
#
# VMN is free software: you can redistribute it and/or modify it under
# the terms of the GNU Affero General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.
#
# VMN is distributed in the hope that it will be useful, but WITHOUT
# ANY WARRANTY; without even the implied warranty of MERCHANTABILITY
# or FITNESS FOR A PARTICULAR PURPOSE. See the GNU Affero General
# Public License for more details.
#
# You should have received a copy of the GNU Affero General Public
# License along with VMN. If not, see <http://www.gnu.org/licenses/>.

.PHONY: install uninstall

# We use either sudo or doas depending on what is available.
HAS_SUDO := $(shell command -v sudo 2> /dev/null)
HAS_DOAS := $(shell command -v doas 2> /dev/null)

ifndef HAS_SUDO
    ifndef HAS_DOAS
        $(error "Finds neither sudo or doas. Please edit the Makefile.")
    else
        SUDO:=doas
    endif
else
    SUDO:=sudo
endif

# We use the versions of the packages that are in this directory.
GMPMEE_TAR=$(shell ls -1 *.tar.gz | grep verificatum-gmpmee-)
GMPMEE_DIR=$(shell echo $(GMPMEE_TAR) | sed "s/\.tar\.gz//")

VMGJ_TAR=$(shell ls -1 *.tar.gz | grep verificatum-vmgj-)
VMGJ_DIR=$(shell echo $(VMGJ_TAR) | sed "s/\.tar\.gz//")

VEC_TAR=$(shell ls -1 *.tar.gz | grep verificatum-vec-)
VEC_DIR=$(shell echo $(VEC_TAR) | sed "s/\.tar\.gz//")

VECJ_TAR=$(shell ls -1 *.tar.gz | grep verificatum-vecj-)
VECJ_DIR=$(shell echo $(VECJ_TAR) | sed "s/\.tar\.gz//")

VCR_TAR=$(shell ls -1 *.tar.gz | grep verificatum-vcr-)
VCR_DIR=$(shell echo $(VCR_TAR) | sed "s/\.tar\.gz//")

VMN_TAR=$(shell ls -1 *.tar.gz | grep verificatum-vmn-)
VMN_DIR=$(shell echo $(VMN_TAR) | sed "s/\.tar\.gz//")

# Untar, configure, make, and sudo make install each package in the
# right dependency order.
in_gmpmee: .in_gmpmee.stamp
.in_gmpmee.stamp:
	tar xvfz $(GMPMEE_TAR)
	cd $(GMPMEE_DIR); ./configure; $(MAKE); $(SUDO) $(MAKE) install
	./update_lib_cache
	touch .in_gmpmee.stamp

in_vmgj: .in_vmgj.stamp
.in_vmgj.stamp: .in_gmpmee.stamp
	tar xvfz $(VMGJ_TAR)
	cd $(VMGJ_DIR); ./configure; $(MAKE); $(SUDO) $(MAKE) install
	./update_lib_cache
	touch .in_vmgj.stamp

in_vec: .in_vec.stamp
.in_vec.stamp:
	tar xvfz $(VEC_TAR)
	cd $(VEC_DIR); ./configure; $(MAKE); $(SUDO) $(MAKE) install
	./update_lib_cache
	touch .in_vec.stamp

in_vecj: .in_vecj.stamp
.in_vecj.stamp: .in_vec.stamp
	tar xvfz $(VECJ_TAR)
	cd $(VECJ_DIR); ./configure; $(MAKE); $(SUDO) $(MAKE) install
	touch .in_vecj.stamp

in_vcr: .in_vcr.stamp
.in_vcr.stamp: .in_vmgj.stamp .in_vecj.stamp
	tar xvfz $(VCR_TAR)
	cd $(VCR_DIR); ./configure --enable-vmgj --enable-vecj; $(MAKE); $(SUDO) $(MAKE) install
	./update_lib_cache
	vog -rndinit RandomDevice /dev/urandom
	touch .in_vcr.stamp

in_vmn: .in_vmn.stamp
.in_vmn.stamp: .in_vcr.stamp
	tar xvfz $(VMN_TAR)
	cd $(VMN_DIR); ./configure; $(MAKE); $(SUDO) $(MAKE) install
	touch .in_vmn.stamp

install: in_vmn

check:
	cd $(GMPMEE_DIR); $(MAKE) check; cd -
	cd $(VMGJ_DIR); $(MAKE) check; cd -
	cd $(VEC_DIR); $(MAKE) check; cd -
	cd $(VECJ_DIR); $(MAKE) check; cd -
	cd $(VCR_DIR); $(MAKE) check; cd -
	cd $(VMN_DIR); $(MAKE) check; cd -
	rm -f .*.stamp

demo:
	cd $(VMN_DIR)/demo/mixnet; ./demo

uninstall:
	cd $(GMPMEE_DIR); $(SUDO) $(MAKE) uninstall; cd -
	cd $(VMGJ_DIR); $(SUDO) $(MAKE) uninstall; cd -
	cd $(VEC_DIR); $(SUDO) $(MAKE) uninstall; cd -
	cd $(VECJ_DIR); $(SUDO) $(MAKE) uninstall; cd -
	cd $(VCR_DIR); $(SUDO) $(MAKE) uninstall; cd -
	cd $(VMN_DIR); $(SUDO) $(MAKE) uninstall; cd -
	rm -f .*.stamp
	rm -f $(HOME)/.verificatum_random_source
