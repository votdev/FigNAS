PORTNAME=		inadyn-mt
PORTVERSION=	02.28.10
PORTREVISION?=  0
CATEGORIES=		dns
COMMENT=		A simple DYNAMIC DNS client
MAINTAINER=		zoon01@xigmanas.com

MASTER_SITES=	SF/${PORTNAME}/${PORTNAME}/${PORTNAME}.v.${PORTVERSION}
DISTNAME=			${PORTNAME}.v.${PORTVERSION}

WRKSRC=				${WRKDIR}/${PORTNAME}.v.${PORTVERSION}
USE_DOS2UNIX=		yes
GNU_CONFIGURE=	yes

CONFIGURE_ARGS+=	--disable-sound

do-install:
	@${INSTALL_PROGRAM} -v ${WRKSRC}/src/inadyn-mt ${XIGMANAS_ROOTFS}/usr/local/bin/inadyn
	@${INSTALL_SCRIPT} -v ${FILESDIR}/inadyn.in ${XIGMANAS_ROOTFS}/etc/rc.d/inadyn

.include <bsd.port.mk>