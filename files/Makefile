
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

# We use the versions of the packages that are in this directory.
GMPMEE_TAR=$(shell ls *.tar.gz | grep gmpmee)
GMPMEE_DIR=$(shell echo $(GMPMEE_TAR) | sed "s/\.tar\.gz//")

VMGJ_TAR=$(shell ls *.tar.gz | grep vmgj)
VMGJ_DIR=$(shell echo $(VMGJ_TAR) | sed "s/\.tar\.gz//")

VEC_TAR=$(shell ls *.tar.gz | grep vec-)
VEC_DIR=$(shell echo $(VEC_TAR) | sed "s/\.tar\.gz//")

VECJ_TAR=$(shell ls *.tar.gz | grep vecj)
VECJ_DIR=$(shell echo $(VECJ_TAR) | sed "s/\.tar\.gz//")

VCR_TAR=$(shell ls *.tar.gz | grep vcr)
VCR_DIR=$(shell echo $(VCR_TAR) | sed "s/\.tar\.gz//")

VMN_TAR=$(shell ls *.tar.gz | grep vmn)
VMN_DIR=$(shell echo $(VMN_TAR) | sed "s/\.tar\.gz//")

install_gmpmee: .install_gmpmee.stamp
.install_gmpmee.stamp:
	tar xvfz $(GMPMEE_TAR); cd ${GMPMEE_DIR}; ./configure; make; sudo make install
	./update_lib_cache
	touch .install_gmpmee.stamp

install_vmgj: .install_vmgj.stamp
.install_vmgj.stamp: .install_gmpmee.stamp
	tar xvfz $(VMGJ_TAR); cd ${VMGJ_DIR}; ./configure; make; sudo make install
	./update_lib_cache
	touch .install_vmgj.stamp

install_vec: .install_vec.stamp
.install_vec.stamp:
	tar xvfz $(VEC_TAR); cd ${VEC_DIR}; ./configure; make; sudo make install
	./update_lib_cache
	touch .install_vec.stamp

install_vecj: .install_vecj.stamp
.install_vecj.stamp: .install_vec.stamp
	tar xvfz $(VECJ_TAR); cd ${VECJ_DIR}; ./configure; make; sudo make install
	touch .install_vecj.stamp

install_vcr: .install_vcr.stamp
.install_vcr.stamp: .install_vmgj.stamp .install_vecj.stamp
	tar xvfz $(VCR_TAR); cd ${VCR_DIR}; ./configure --enable-vmgj --enable-vecj; make; sudo make install
	./update_lib_cache
	vog -rndinit RandomDevice /dev/urandom
	touch .install_vcr.stamp

install_vmn: .install_vmn.stamp
.install_vmn.stamp: .install_vcr.stamp
	tar xvfz $(VMN_TAR); cd ${VMN_DIR}; ./configure; make; sudo make install
	touch .install_vmn.stamp

install: install_vmn

check:
	cd ${GMPMEE_DIR}; make check; cd -; done
	cd ${VMGJ_DIR}; make check; cd -; done
	cd ${VEC_DIR}; make check; cd -; done
	cd ${VECJ_DIR}; make check; cd -; done
	cd ${VCR_DIR}; make check; cd -; done
	cd ${VMN_DIR}; make check; cd -; done
	rm -f .*.stamp

demo:
	cd ${VMN_DIR}/demo/mixnet; ./demo

uninstall:
	cd ${GMPMEE_DIR}; sudo make uninstall; cd -; done
	cd ${VMGJ_DIR}; sudo make uninstall; cd -; done
	cd ${VEC_DIR}; sudo make uninstall; cd -; done
	cd ${VECJ_DIR}; sudo make uninstall; cd -; done
	cd ${VCR_DIR}; sudo make uninstall; cd -; done
	cd ${VMN_DIR}; sudo make uninstall; cd -; done
	rm -f .*.stamp
