#
# Open Chinese Convert
#
# Copyright 2010 BYVoid <byvoid1@gmail.com>
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#

SUBDIRS = \
	data \
	doc \
	src \
	m4 \
	po \
	test \
	$(NULL)

ACLOCAL_AMFLAGS = -I m4

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = opencc.pc

EXTRA_DIST = \
	opencc.pc.in \
	autogen.sh \
	$(NULL)

noinst_DIST = \
	$(NULL)

DISTCLEANFILES = \
	po/stamp-it \
	package \
	$(NULL)

rpm: dist @PACKAGE_NAME@.spec
	rpmbuild -ba --clean \
	--define "_sourcedir `pwd`" \
	--define "_builddir `pwd`/package/rpm" \
	--define "_srcrpmdir `pwd`/package/rpm" \
	--define "_rpmdir `pwd`/package/rpm" \
	--define "_specdir `pwd`/package/rpm" \
	--nodeps \
	@PACKAGE_NAME@.spec

debsource: dist debian
	$(AM_V_GEN) \
	( \
		mkdir -p package/debsource ;\
		cd package/debsource ;\
		rm -rf * ;\
		tar xf ../../$(distdir).tar.gz ;\
		cp ../../$(distdir).tar.gz @PACKAGE@_@VERSION@.orig.tar.gz ;\
		cd $(distdir) ;\
		cp -r ../../../debian . ;\
		cd debian ;\
		debuild -S -sa -tc ;\
		cd ../.. ;\
		rm -rf $(distdir) ;\
	)

deb: debsource
	$(AM_V_GEN) \
	( \
		mkdir -p package/deb ;\
		cd package/deb ;\
		rm -rf * ;\
		tar xf ../../$(distdir).tar.gz ;\
		cp ../../$(distdir).tar.gz @PACKAGE@_@VERSION@.orig.tar.gz ;\
		cd $(distdir) ;\
		cp -r ../../../debian . ;\
		cd debian ;\
		debuild -sa -tc ;\
		cd ../.. ;\
		rm -rf $(distdir) ;\
	)
