# $OpenBSD: Makefile,v 1.20 2017/11/21 00:13:02 naddy Exp $

COMMENT =		native Gtk+ Twitter client

V =			1.7.3
DISTNAME =		corebird-${V}
MASTER_SITES =		https://github.com/baedert/corebird/releases/download/${V}/
REVISION =		0

EXTRACT_SUFX =		.tar.xz
CATEGORIES =		net

HOMEPAGE =		https://corebird.baedert.org/

MAINTAINER =		Adam Wolk <awolk@openbsd.org>

# GPLv3
PERMIT_PACKAGE_CDROM =	Yes

WANTLIB += Xtst X11 Xcomposite Xcursor Xdamage Xext Xfixes Xi
WANTLIB += Xinerama Xrandr Xrender atk-1.0 atk-bridge-2.0 atspi
WANTLIB += c cairo cairo-gobject dbus-1 enchant epoxy expat ffi
WANTLIB += fontconfig freetype gdk-3 gdk_pixbuf-2.0 gio-2.0 glib-2.0
WANTLIB += gmodule-2.0 gobject-2.0 graphite2 gspell-1 gstbase-1.0
WANTLIB += gstreamer-1.0 gstvideo-1.0 gthread-2.0 gtk-3 harfbuzz iconv intl
WANTLIB += json-glib-1.0 lzma m orc-0.4 pango-1.0 pangocairo-1.0
WANTLIB += pangoft2-1.0 pcre pixman-1 png pthread
WANTLIB += soup-2.4 sqlite3 ${COMPILER_LIBCXX} xcb
WANTLIB += xcb-render xcb-shm xml2 z

MODULES =		devel/dconf \
			x11/gnome

MODGNOME_TOOLS =	desktop-file-utils \
			gtk-update-icon-cache \
			vala

BUILD_DEPENDS =		devel/gettext-tools

LIB_DEPENDS =		databases/sqlite3 \
			devel/json-glib \
			devel/libsoup>=2.4 \
			devel/orc \
			multimedia/gstreamer1/core \
			multimedia/gstreamer1/plugins-base \
			textproc/gspell \
			x11/gtk+3

RUN_DEPENDS =		multimedia/gstreamer1/plugins-bad \
			multimedia/gstreamer1/plugins-good \
			multimedia/gstreamer1/plugins-libav \

CONFIGURE_STYLE =	gnu
USE_GMAKE =		Yes

TEST_ENV =		HOME=${WRKDIR}/tests
TEST_IS_INTERACTIVE =	x11

SEPARATE_BUILD =	Yes

pre-test:
	mkdir -p ${WRKDIR}/tests/.config/corebird

.include <bsd.port.mk>
