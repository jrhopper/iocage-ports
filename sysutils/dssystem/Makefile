# $FreeBSD$

PORTNAME=	dssystem
PORTVERSION=	14.1
PORTREVISION=	10
CATEGORIES=	sysutils
MASTER_SITES=	https://cdn1.tn.ixsystems.com/asigra/14.1/hotfixes/ \
		https://asigra-f611.kxcdn.com/14.1/hotfixes/
DISTNAME=	DS-System_14_1_0_200_FreeBSD
EXTRACT_SUFX=	.zip

MAINTAINER=	wg@FreeBSD.org
COMMENT=	Award cloud backup and restore server application

ONLY_FOR_ARCHS=	amd64

RUN_DEPENDS=	ca_root_nss>0:security/ca_root_nss \
		icu>0:devel/icu \
		indexinfo>0:print/indexinfo \
		libxml2>0:textproc/libxml2 \
		openldap-sasl-client>2.4.0:net/openldap24-sasl-client \
		nss-pam-ldapd-sasl>0:net/nss-pam-ldapd-sasl

NO_BUILD=	yes
USES=		gettext-runtime perl5

USE_RC_SUBR=	dssystem

EXTRACT_AFTER_ARGS=	-C ${STAGEDIR}

pre-extract:
	${MKDIR} ${STAGEDIR}

post-extract:
	@${FIND} ${STAGEDIR}/${DISTNAME}/ -name "*txz" -exec tar -C ${STAGEDIR} -xzf {} \;
	@${RM} -rf ${STAGEDIR}/${DISTNAME}

do-install:
	${CP} ${FILESDIR}/dssystem_install.ini ${STAGEDIR}
	(cd ${STAGEDIR}${PREFIX}/ds-system; ${FIND} . \( -type f -o -type l \) \
		| ${SED} -e 's,^\./,,g' \
		| ${AWK} '{print length, $$0}' | ${SORT} -rn \
		| ${AWK} '{print "ds-system/"$$2 }' >> ${TMPPLIST})

.include <bsd.port.mk>
