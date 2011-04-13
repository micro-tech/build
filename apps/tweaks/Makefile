NAME     = tweaks
TITLE    = Tweaks
APP_ID   = org.webosinternals.${NAME}
SRV_ID   = org.webosinternals.${NAME}.prefs
SIGNER   = org.webosinternals
BLDFLAGS = -p
VERSION  = 1.1.0
TYPE	 = Application
CATEGORY = System Utilities
HOMEPAGE = http://www.webos-internals.org/wiki/Application:Tweaks
ICON	 = http://www.webos-internals.org/images/2/2e/Tweaks-icon.png
DESCRIPTION = Tweaks for your webOS device.
MINWEBOSVERSION = 2.0.0
CHANGELOG = \
1.1.0: Allow for the tweaks json file to override the owner value.<br>\
1.0.0: Initial public release.

SCREENSHOTS = [\
\"http://www.webos-internals.org/images/d/de/Tweaks_ss1.png\" ]

LICENSE  = GPL v2 Open Source

SRC_GIT = git://git.webos-internals.org/applications/tweaks.git

.PHONY: package
package: ipkgs/${APP_ID}_${VERSION}_all.ipk
include ../../support/package.mk

include ../../support/download.mk

.PHONY: unpack
unpack: build/.unpacked-${VERSION}

build/.unpacked-${VERSION}: ${DL_DIR}/${NAME}-${VERSION}.tar.gz
	rm -rf build
	mkdir -p build/src
	tar -C build/src -xf ${DL_DIR}/${NAME}-${VERSION}.tar.gz
	touch $@

.PHONY: build
build: build/.built-${VERSION}

build/.built-${VERSION}: build/all.built-${VERSION}
	touch $@

build/%.built-${VERSION}: build/.unpacked-${VERSION}
	rm -rf build/$*
	mkdir -p build/$*/usr/palm/applications/${APP_ID}
	cp -r build/src/* build/$*/usr/palm/applications/${APP_ID}/
	mkdir -p build/$*/usr/palm/services/${SRV_ID}
	cp -r build/src/node-service/* build/$*/usr/palm/services/${SRV_ID}/
	rm -rf build/$*/usr/palm/applications/${APP_ID}/node-service
	mkdir -p build/$*/usr/palm/packages/${APP_ID}
	cp -r build/src/package/* build/$*/usr/palm/packages/${APP_ID}/
	rm -rf build/$*/usr/palm/applications/${APP_ID}/package
	touch $@

clobber::
	rm -rf build