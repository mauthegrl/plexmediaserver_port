# $FreeBSD$

PORTNAME=	plexmediaserver
PORTVERSION=	0.9.7.23.0
CATEGORIES=	multimedia
MASTER_SITES=	http://www.plexapp.com/elan/
DISTFILES=	PlexMediaServer-${PORTVERSION}-${GH_COMMIT}.tar.bz2
SUPPORT_PATH?=	${PREFIX}/lib

MAINTAINER=	plexmaintainer@k-moeller.dk
COMMENT=	Plex Media Server

GH_COMMIT=	8e6b2a8

NO_BUILD=	yes
WRKSRC=		${WRKDIR}/PlexMediaServer-${PORTVERSION}-${GH_COMMIT}

USE_RC_SUBR=	plexmediaserver

SUB_FILES=	plexmediaserver
SUB_LIST=	SUPPORT_PATH=${SUPPORT_PATH} SCRIPT_PATH="${DATADIR}"


post-patch:
	${REINPLACE_CMD} -e 's|%%SCRIPT_PATH%%|"${DATADIR}"|' ${PATCH_WRKSRC}/start.sh
	${REINPLACE_CMD} -e 's|%%SUPPORT_PATH%%|"${SUPPORT_PATH}"|' ${PATCH_WRKSRC}/start.sh

do-install:
	(cd ${WRKSRC} && ${COPYTREE_SHARE} Resources ${DATADIR})
	${INSTALL_PROGRAM} ${WRKSRC}/Plex\ DLNA\ Server ${DATADIR}
	${INSTALL_PROGRAM} ${WRKSRC}/Plex\ Media\ Scanner ${DATADIR}
	${INSTALL_PROGRAM} ${WRKSRC}/Plex\ Media\ Server ${DATADIR}
	${INSTALL_SCRIPT} ${WRKSRC}/start.sh ${DATADIR}
	${INSTALL_LIB} ${WRKSRC}/lib* ${DATADIR}
	${CHMOD} a+x ${DATADIR}/Resources/rsync
	${CHMOD} a+x ${DATADIR}/Resources/Plex\ New\ Transcoder
	${CHMOD} a+x ${DATADIR}/Resources/Plex\ Transcoder
	${CHMOD} a+x ${DATADIR}/Resources/Python/bin/python
	${LN} -s ${DATADIR}/libpython2.7.so.1 ${DATADIR}/libpython2.7.so

.include <bsd.port.mk>
