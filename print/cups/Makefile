# $OpenBSD: Makefile,v 1.233 2018/01/14 14:42:18 rpe Exp $

COMMENT-main=		Common Unix Printing System
COMMENT-libs=		CUPS libraries and headers

VERSION=		2.2.6
GH_ACCOUNT=		apple
GH_PROJECT=		cups
GH_TAGNAME=		v${VERSION}

PKGNAME-main=		cups-${VERSION}
PKGNAME-libs=		cups-libs-${VERSION}

REVISION-main=		3

CATEGORIES=		print sysutils

# config-scripts/cups-sharedlibs.m4
SHARED_LIBS+=  cupsimage       5.1 # so.2
SHARED_LIBS+=  cups            6.4 # so.2
SHARED_LIBS+=  cupscgi         1.1 # so.1
SHARED_LIBS+=  cupsmime        1.2 # so.1
SHARED_LIBS+=  cupsppdc        1.2 # so.1

HOMEPAGE=		http://www.cups.org/

MAINTAINER=		Antoine Jacoutot <ajacoutot@openbsd.org>

# GPLv2 - LGPLv2
PERMIT_PACKAGE_CDROM=	Yes

WANTLIB += avahi-client avahi-common gnutls iconv m pthread ${COMPILER_LIBCXX} z

WANTLIB-main += ${WANTLIB}
WANTLIB-main += c cups cupscgi cupsimage cupsmime cupsppdc dbus-1 usb-1.0

MULTI_PACKAGES=		-main -libs

BUILD_DEPENDS=		${MODGNU_AUTOMAKE_DEPENDS} \
			${MODGNU_AUTOCONF_DEPENDS}

# bootstrap prevents a cyclic dep: gtk+{2,3}->cups->avahi->gtk+{2,3}
LIB_DEPENDS-libs=	net/avahi,no_gui,bootstrap \
			security/gnutls

LIB_DEPENDS-main=	${BASE_PKGPATH},-libs=${VERSION} \
			devel/libusb1

RUN_DEPENDS-main=	print/cups-filters

# optional for now
#RUN_DEPENDS-main +=	graphics/colord

# we don't install the desktop file
#BUILD_DEPENDS +=	devel/xdg-utils
#RUN_DEPENDS-main +=	devel/xdg-utils

LIBS_ENV=		LIBcups_VERSION=${LIBcups_VERSION} \
			LIBcupscgi_VERSION=${LIBcupscgi_VERSION} \
			LIBcupsimage_VERSION=${LIBcupsimage_VERSION} \
			LIBcupsmime_VERSION=${LIBcupsmime_VERSION} \
			LIBcupsppdc_VERSION=${LIBcupsppdc_VERSION} \

FAKE_FLAGS=		BUILDROOT=${WRKINST} \
			DBUSDIR=${PREFIX}/share/examples/cups/dbus-1 \
			ICONDIR=${PREFIX}/share/icons \
			MENUDIR=${PREFIX}/share/applications \
			SERVERROOT=${WRKINST}${PREFIX}/share/examples/cups

AUTOCONF_VERSION= 	2.69
AUTOMAKE_VERSION= 	1.15

USE_GMAKE=		Yes

MAKE_ENV=		${LIBS_ENV}

CONFIGURE_ENV=		CPPFLAGS="-I${LOCALBASE}/include" \
			LDFLAGS="-L${LOCALBASE}/lib" \
			${LIBS_ENV}

CONFIGURE_STYLE=	gnu
CONFIGURE_ARGS=		--enable-static \
			--disable-libtool_unsupported \
			--with-cups-group=_cups \
			--with-cups-user=_cups \
			--with-system-groups=wheel \
			--with-dbusdir=${SYSCONFDIR}/dbus-1 \
			--with-printcap=${SYSCONFDIR}/cups/printcap \
			--with-smbconfigfile="samba://${SYSCONFDIR}/samba/smb.conf" \
			--disable-cdsassl \
			--disable-pam \
			--disable-systemd \
			--without-java \
			--without-php \
			--without-python

pre-configure:
	cd ${WRKSRC} && \
		AUTOMAKE_VERSION=${AUTOMAKE_VERSION} AUTOCONF_VERSION=${AUTOCONF_VERSION} aclocal -I config-scripts
	cd ${WRKSRC} && \
		AUTOMAKE_VERSION=${AUTOMAKE_VERSION} AUTOCONF_VERSION=${AUTOCONF_VERSION} autoconf -I config-scripts
	${SUBST_CMD} ${WRKSRC}/{Makedefs.in,cups/Makefile}

post-configure:
	cd ${WRKBUILD} && sed -i 's|\$${DESTDIR}||g' \
		config.h cups-config man/*.man

post-install:
	ln -sf ${LOCALBASE}/bin/smbspool \
		${PREFIX}/libexec/cups/backend/smb
# used to register as @sample: classes.conf, client.conf, lpoptions,
# printers.conf and subscriptions.conf in the PLIST
	touch ${PREFIX}/share/examples/cups/empty.conf
# Remove files now part of cups-filters
	rm -f ${PREFIX}/share/cups/banners/*
	rm -f ${PREFIX}/share/cups/data/testprint

# Remove desktop file and icons; we don't really need them (it's just a
# launcher for http://localhost:631 and we may actually want to
# configure a remote server); this is needed to prevent a dependency
# loop: cups->gtk+3,-guic->cups
	rm -rf ${PREFIX}/share/icons
	rm -rf ${PREFIX}/share/applications

# Remove systemV files
	rm -rf ${WRKINST}/etc/rc.d/{init,rc*}.d

.include <bsd.port.mk>
