# $OpenBSD: Makefile,v 1.13 2018/01/19 09:52:12 landry Exp $

COMMENT =	user interface library from pwmt
DISTNAME =	girara-0.2.8

SHARED_LIBS +=	girara-gtk3 1.0 # 2.3

CATEGORIES =	x11
HOMEPAGE =	http://pwmt.org/projects/girara/

# zlib
PERMIT_PACKAGE_CDROM =Yes

WANTLIB += atk-1.0 cairo cairo-gobject gdk-3 gdk_pixbuf-2.0 gio-2.0
WANTLIB += glib-2.0 gobject-2.0 gtk-3 intl json-c m notify pango-1.0
WANTLIB += pangocairo-1.0

MASTER_SITES =	http://pwmt.org/projects/girara/download/

BUILD_DEPENDS =	devel/gettext-tools
LIB_DEPENDS =	x11/gtk+3 \
		devel/json-c \
		devel/libnotify

# c11
COMPILER =	base-clang ports-gcc
COMPILER_LANGS =	c

USE_GMAKE =	Yes

MAKE_FLAGS +=	VERBOSE=1 TPUT=true COLOR=0
MAKE_FLAGS +=	SOVERSION=${LIBgirara-gtk3_VERSION}

FAKE_FLAGS +=	PREFIX=${TRUEPREFIX}

TEST_TARGET =	test
TEST_DEPENDS =	devel/check
TEST_FLAGS +=	VERBOSE=1
TEST_FLAGS +=	HOME=${WRKDIR}
TEST_IS_INTERACTIVE =X11

.include <bsd.port.mk>
