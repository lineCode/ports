# $OpenBSD: Makefile,v 1.15 2017/11/21 00:13:01 naddy Exp $

COMMENT=		fast and simple image viewer

DISTNAME=		viewnior-1.6
REVISION=		2

CATEGORIES=		graphics x11

HOMEPAGE=		http://siyanpanayotov.com/project/viewnior/

# GPLv3
PERMIT_PACKAGE_CDROM=	Yes

WANTLIB += X11 Xcomposite Xcursor Xdamage Xext Xfixes Xi Xinerama
WANTLIB += Xrandr Xrender atk-1.0 c cairo exiv2 expat ffi fontconfig
WANTLIB += freetype gdk-x11-2.0 gdk_pixbuf-2.0 gio-2.0 glib-2.0
WANTLIB += gmodule-2.0 gobject-2.0 graphite2 gthread-2.0 gtk-x11-2.0
WANTLIB += harfbuzz iconv intl m pango-1.0 pangocairo-1.0 pangoft2-1.0 pcre
WANTLIB += pixman-1 png pthread ${COMPILER_LIBCXX} xcb xcb-render
WANTLIB += xcb-shm z

MASTER_SITES=		https://github.com/xsisqox/Viewnior/archive/

MODULES=		textproc/intltool

LIB_DEPENDS=		graphics/exiv2 \
			x11/gtk+2

RUN_DEPENDS=		devel/desktop-file-utils \
			x11/gtk+3,-guic

USE_GMAKE=		yes

WRKDIST=		${WRKDIR}/Viewnior-${DISTNAME}

# detect images using mimetype
BUILD_DEPENDS +=	misc/shared-mime-info
RUN_DEPENDS +=		misc/shared-mime-info

AUTOCONF_VERSION=	2.69
AUTOMAKE_VERSION=	1.15
BUILD_DEPENDS +=	${MODGNU_AUTOCONF_DEPENDS} \
			${MODGNU_AUTOMAKE_DEPENDS} \
			devel/libtool

CONFIGURE_STYLE=	gnu
CONFIGURE_ENV=		CPPFLAGS="-I${LOCALBASE}/include" \
			LDFLAGS="-L${LOCALBASE}/lib"

pre-configure:
	cd ${WRKSRC} && \
		AUTOCONF_VERSION=${AUTOCONF_VERSION} \
		AUTOMAKE_VERSION=${AUTOMAKE_VERSION} \
		autoreconf -fi

.include <bsd.port.mk>
