# $OpenBSD: Makefile,v 1.21 2017/11/21 00:13:04 naddy Exp $

COMMENT =		HTML form validation, generation, and conversion

MODPY_EGG_VERSION =	1.2.4
DISTNAME =		FormEncode-${MODPY_EGG_VERSION}
PKGNAME =		py-formencode-${MODPY_EGG_VERSION}
REVISION =		2

CATEGORIES =		www

HOMEPAGE =		http://www.formencode.org/

# PSF
PERMIT_PACKAGE_CDROM =	Yes

MODPY_PI =		Yes

MODULES =		lang/python

TEST_DEPENDS =	databases/py-sqlobject \
			devel/py-nose

MODPY_SETUPTOOLS =	Yes

post-install:
	${INSTALL_DATA_DIR} ${PREFIX}/share/doc/py-formencode
	cd ${WRKSRC}/docs && pax -rw * ${PREFIX}/share/doc/py-formencode/

do-test:
	cd ${WRKSRC} && ${LOCALBASE}/bin/nosetests tests

.include <bsd.port.mk>
