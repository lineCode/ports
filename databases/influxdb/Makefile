# $OpenBSD: Makefile,v 1.2 2018/01/11 19:27:01 rpe Exp $

COMMENT =	time-series datastore for metrics, events, and analytics

V =		1.4.2
DISTNAME =	influxdb-${V}
REVISION =	0

HOMEPAGE =	https://influxdata.com
# selfhosted because we bundle go deps
MASTER_SITES =	https://rhaalovely.net/stuff/

CATEGORIES =		databases

# MIT
PERMIT_PACKAGE_CDROM =	Yes

MODULES =	lang/go

BUILD_DEPENDS =	security/go-crypto \
		textproc/go-text \
		devel/go-sys \
		textproc/xmlto \
		textproc/asciidoc

# our handrolled distfile has the "right" layout already
# disables MODGO_SETUP_WORKSPACE
CONFIGURE_STYLE =	No
WRKSRC =	${MODGO_WORKSPACE}/src/github.com/influxdata/influxdb
# for patches to apply
WRKDIST =	${WRKSRC}
# for man/Makefile
USE_GMAKE =	Yes
SUBST_VARS =	VARBASE

post-extract:
	cp -r ${LOCALBASE}/${MODGO_SOURCES}/golang.org/x/{crypto,text,sys} \
		${MODGO_WORKSPACE}/src/golang.org/x/

do-build:
	cd ${WRKSRC} && ${MODGO_BUILD_CMD} ./...
	cd ${WRKSRC}/man && ${MAKE_PROGRAM}

do-install:
	${MODGO_INSTALL_TARGET}
	cd ${WRKSRC}/man && ${SETENV} ${MAKE_ENV} ${MAKE_PROGRAM} install
	${INSTALL_DATA_DIR} ${PREFIX}/share/examples/influxdb/
	${INSTALL_DATA} ${WRKSRC}/etc/config.sample.toml \
		${PREFIX}/share/examples/influxdb/

# convenience hackish target to bundle/vendor dependencies
tarball: clean distclean
	mkdir -p ${WRKDIR}/go/src/github.com/influxdata/
	ftp -o ${WRKDIR}/gpm https://raw.githubusercontent.com/pote/gpm/v1.4.0/bin/gpm
	ftp -o ${WRKDIR}/${DISTFILES} https://github.com/influxdata/influxdb/archive/v${V}/${DISTFILES}
	tar -s /influxdb-${V}/influxdb/ -C ${WRKDIR}/go/src/github.com/influxdata/ -xzf ${WRKDIR}/${DISTFILES}
	${SETENV} ${MODGO_ENV} bash ${WRKDIR}/gpm get ${WRKSRC}/Godeps
	find ${WRKDIR}/go -name .git -type d | xargs rm -Rf
	cd ${WRKDIR} && tar -czf /usr/ports/distfiles/${DISTFILES} go

.include <bsd.port.mk>
