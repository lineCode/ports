# $OpenBSD: Makefile,v 1.33 2018/01/20 14:03:39 jsg Exp $

COMMENT=		the Git library, take 2

GH_ACCOUNT =		libgit2
GH_PROJECT =		libgit2
GH_TAGNAME =		v0.26.0

SHARED_LIBS +=  git2                      10.0 # 0.25

MODULES=		devel/cmake \
			lang/python

MODPY_RUNDEP=		No

COMPILER=		base-clang ports-gcc base-gcc
COMPILER_LANGS=		c
# for atomic builtins
MODGCC4_ARCHS=		hppa

# bundles https://github.com/nodejs/http-parser
LIB_DEPENDS=		net/curl \
			security/libssh2

WANTLIB += crypto curl pthread ssh2 ssl z

CONFIGURE_ARGS=		-DCMAKE_C_FLAGS="-I${LOCALBASE}/include" \
			-DCMAKE_EXE_LINKER_FLAGS:STRING="-L${LOCALBASE}/lib" \
			-DCMAKE_SHARED_LINKER_FLAGS:STRING="-L${LOCALBASE}/lib"

.include <bsd.port.mk>
