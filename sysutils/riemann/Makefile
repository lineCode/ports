# $OpenBSD: Makefile,v 1.7 2018/01/11 19:27:10 rpe Exp $

COMMENT=	network event stream processing system

V=		0.2.14
DISTNAME=	riemann-${V}
CATEGORIES=	sysutils
REVISION=	0

HOMEPAGE=	http://riemann.io

MAINTAINER=	Pavel Korovin <p@tristero.se>

# Eclipse Public License Version 1.0 (http://www.eclipse.org/legal/epl-v10.html)
PERMIT_PACKAGE_CDROM=	commercial distribution defend and indemnify clauses
PERMIT_PACKAGE_FTP=	Yes

MASTER_SITES=	https://github.com/riemann/riemann/releases/download/${V}/

EXTRACT_SUFX=	.tar.bz2

MODULES=	java
MODJAVA_VER=	1.8+
MODJAVA_JRERUN=	yes

RUN_DEPENDS=	java/javaPathHelper \
		lang/clojure

NO_BUILD=	Yes
NO_TEST=	Yes

do-install:
	${SUBST_CMD} ${WRKSRC}/bin/riemann ${WRKSRC}/etc/riemann.config
	${INSTALL_DATA_DIR} ${PREFIX}/{bin,lib/riemann,share/examples/riemann}
	${INSTALL_SCRIPT} ${WRKSRC}/bin/riemann ${PREFIX}/bin
	${INSTALL_DATA} ${WRKSRC}/lib/riemann.jar ${PREFIX}/lib/riemann
	${INSTALL_DATA} ${WRKSRC}/etc/riemann.config \
	    ${PREFIX}/share/examples/riemann

.include <bsd.port.mk>
