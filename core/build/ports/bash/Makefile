PORTNAME=		bash
PATCHLEVEL=		11
PORTVERSION=		5.0.${PATCHLEVEL:S/^0//g}
PORTREVISION?=		0
CATEGORIES=		shells

COMMENT=		GNU Project's Bourne Again SHell
MAINTAINER=		zoon01@xigmanas.com

MASTER_SITES=		GNU
DISTNAME=		${PORTNAME}-${PORTVERSION:R}
DIST_SUBDIR=		${PORTNAME}
EXTRACT_ONLY=		${DISTNAME}${EXTRACT_SUFX}

PATCH_SITES=		GNU/${PORTNAME}/${DISTNAME}-patches/
PATCHFILES!=		/usr/bin/jot -s " " -w \
			${PORTNAME}${PORTVERSION:R:S/.//g}-%03d \
			${PATCHLEVEL} 1 ${PATCHLEVEL}

OPTIONS_DEFINE=         HELP NLS
HELP_DESC=		Enable builtin help

GNU_CONFIGURE=  yes
NO_PKG_REGISTER=yes
USES=		  bison
USE_GETTEXT=	  yes
CONFIGURE_ARGS=			--without-bash-malloc \
					--disable-rpath \
					--enable-disabled-builtins \
					--with-libiconv-prefix=${ICONV_PREFIX} \
					--disable-help-builtin \
					--disable-static-link
CPPFLAGS+=	${PTHREAD_CFLAGS} \
					-I${LOCALBASE}/include
LDFLAGS+=				-L${LOCALBASE}/lib
CONFIGURE_ENV=	CPPFLAGS="${CPPFLAGS}" \
					LDFLAGS="${LDFLAGS}" \
					YACC="bison"

.include <bsd.port.pre.mk>

post-patch:
	@${REINPLACE_CMD} -e "s|%%PREFIX%%|${PREFIX}|g" ${WRKSRC}/doc/bash.1

post-configure:
	@${FIND} ${WRKSRC} -name Makefile -print0 | ${XARGS} -0 \
	${REINPLACE_CMD} -e "s|^DESTDIR *=|& ${DESTDIR}|"

pre-build:
	@${ECHO_CMD} $$((${PORTREVISION}-1)) > ${WRKSRC}/.build

do-install:
	@${INSTALL_PROGRAM} -v ${WRKSRC}/bash ${XIGMANAS_ROOTFS}/usr/local/bin
	@${LN} -fsv /usr/local/bin/bash ${XIGMANAS_ROOTFS}/usr/local/bin/rbash
	@${LN} -fsv /usr/local/bin/bash ${XIGMANAS_ROOTFS}/bin/bash

regress: build
	cd ${WRKSRC}; ${SETENV} ${MAKE_ENV} ${MAKE} ${MAKE_ARGS} test

ckp:
	${MAKE} -DPATCH_DEBUG clean patch

cklatest:
	@${ECHO} -n "Currently at: "
	@${MAKE} -V PATCHLEVEL
	-ncftpls \
		${PATCH_SITES:Mftp*:Ox:[1]} \
		| fgrep -v .sig | ${TAIL}

.include <bsd.port.post.mk>
