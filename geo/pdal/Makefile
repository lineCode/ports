# $OpenBSD: Makefile,v 1.5 2018/02/12 20:47:35 landry Exp $

COMMENT =	translator library for point cloud formats

GH_TAGNAME =	1.6
GH_ACCOUNT =	PDAL
GH_PROJECT =	PDAL
DISTNAME =	${GH_PROJECT:L}-${GH_TAGNAME}
REVISION =	0

SHARED_LIBS =	pdal_base 1.0 # 6.1
SHARED_LIBS +=  pdal_util 0.1 # 6.1

CATEGORIES =	geo devel textproc

HOMEPAGE =	https://pdal.io/

MAINTAINER =	Landry Breuil <landry@openbsd.org>

# BSD
PERMIT_PACKAGE_CDROM =	Yes

MODULES =	devel/cmake lang/python

# uses std=c++0x
COMPILER =	base-clang ports-gcc

MODPY_VERSION =	${MODPY_DEFAULT_VERSION_3}
BUILD_DEPENDS =	math/py-numpy,${MODPY_FLAVOR}
LIB_DEPENDS =	${MODPY_LIB_DEPENDS} \
		geo/gdal \
		devel/jsoncpp \
		databases/postgresql \
		net/curl

WANTLIB +=	c curl gdal geos geotiff jsoncpp m pq pthread ${MODPY_WANTLIB}
WANTLIB +=	xml2 z
WANTLIB += ${COMPILER_LIBCXX}

CONFIGURE_ARGS =	\
	-DJSONCPP_INCLUDE_DIR=${LOCALBASE}/include/jsoncpp/ \
	-DPDAL_PLUGIN_INSTALL_PATH=${LOCALBASE}/share/pdal/plugins \
	-DNUMPY_INCLUDE_DIR=${MODPY_SITEPKG}/numpy/core/include/ \
	-DNUMPY_VERSION=1.9 \
	-DBUILD_PLUGIN_PYTHON=ON

post-extract:
	rm ${WRKSRC}/cmake/modules/FindGDAL.cmake

# needs load extension
# -DBUILD_PLUGIN_SQLITE=ON

.include <bsd.port.mk>
