# $OpenBSD: Makefile,v 1.7 2017/01/03 19:21:18 landry Exp $

COMMENT =		SVG scrubber
MODPY_EGG_VERSION =	0.35
REVISION =		1
CATEGORIES =		graphics
MAINTAINER =		Dmitrij D. Czarkoff <czarkoff@openbsd.org>
HOMEPAGE =		http://www.codedread.com/scour/

PERMIT_PACKAGE_CDROM =	Yes

GH_ACCOUNT =		codedread
GH_PROJECT =		scour
GH_TAGNAME =		v${MODPY_EGG_VERSION}

MODULES =		lang/python
MODPY_SETUPTOOLS =	Yes
MODPY_VERSION =		${MODPY_DEFAULT_VERSION_3}
RUN_DEPENDS =		devel/py-six${MODPY_FLAVOR}

do-test:
	@cd ${WRKDIST} && ${MODPY_BIN} testscour.py
	@cd ${WRKDIST} && ${MODPY_BIN} testcss.py

.include <bsd.port.mk>
