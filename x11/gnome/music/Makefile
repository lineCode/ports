# $OpenBSD: Makefile,v 1.49 2018/02/09 22:47:34 ajacoutot Exp $

COMMENT=		GNOME music playing application

GNOME_PROJECT=		gnome-music
GNOME_VERSION=		3.26.2

# GPLv2+
PERMIT_PACKAGE_CDROM=	Yes

WANTLIB += Xtst X11 Xcomposite Xcursor Xdamage Xext Xfixes Xi
WANTLIB += Xinerama Xrandr Xrender atk-1.0 atk-bridge-2.0 atspi
WANTLIB += cairo cairo-gobject dbus-1 epoxy expat ffi fontconfig
WANTLIB += freetype gdk-3 gdk_pixbuf-2.0 gio-2.0 glib-2.0 gmodule-2.0
WANTLIB += gobject-2.0 graphite2 gthread-2.0 gtk-3 harfbuzz iconv
WANTLIB += intl m pango-1.0 pangocairo-1.0 pangoft2-1.0 pcre pixman-1
WANTLIB += png pthread xcb xcb-render xcb-shm z

MODULES=		devel/dconf \
			lang/python \
			x11/gnome

MODGNOME_TOOLS +=	desktop-file-utils gobject-introspection yelp
MODGNOME_TOOLS +=	gtk-update-icon-cache

MODPY_VERSION=		${MODPY_DEFAULT_VERSION_3}

LIB_DEPENDS=		x11/gtk+3

BUILD_DEPENDS=		devel/py-gobject3${MODPY_FLAVOR} \
			x11/gnome/grilo \
			x11/gnome/libmediaart \
			x11/gnome/tracker

RUN_DEPENDS=		devel/py-gobject3${MODPY_FLAVOR} \
			www/py-requests${MODPY_FLAVOR} \
			x11/gnome/grilo \
			x11/gnome/libmediaart \
			x11/gnome/tracker

# sndio(7) support
RUN_DEPENDS +=	multimedia/gstreamer1/plugins-base

CONFIGURE_STYLE=	gnu

post-install:
	rm ${PREFIX}/lib/gnome-music/*.{a,la}

.include <bsd.port.mk>
