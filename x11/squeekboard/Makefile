# $FreeBSD$

PORTNAME=	squeekboard
DISTVERSIONPREFIX=	v
DISTVERSION=	1.5.0
CATEGORIES=	x11

MAINTAINER=	jbeich@FreeBSD.org
COMMENT=	On-screen keyboard for Wayland

LICENSE=	GPLv3
LICENSE_FILE=	${WRKSRC}/COPYING

BROKEN_FreeBSD_11=	requires getrandom()

BUILD_DEPENDS=	wayland-protocols>=1.12:graphics/wayland-protocols
LIB_DEPENDS=	libwayland-client.so:graphics/wayland \
		libcroco-0.6.so:textproc/libcroco \
		libxkbcommon.so:x11/libxkbcommon
RUN_DEPENDS=	gsettings-desktop-schemas>0:devel/gsettings-desktop-schemas

USES=		cargo compiler:c11 gettext-tools gnome meson pkgconfig
USE_GITLAB=	yes
USE_GNOME=	cairo gdkpixbuf2 gtk30
GL_SITE=	https://source.puri.sm
GL_ACCOUNT=	Librem5
GL_COMMIT=	d76deb0655fdf4f60e29dc74bca29efb380d9a8f
MAKE_ENV=	${CARGO_ENV}
PLIST_FILES=	bin/${PORTNAME} \
		bin/${PORTNAME}-test-layout \
		share/applications/sm.puri.Squeekboard.desktop

CARGO_CRATES=	aho-corasick-0.7.6 \
		ansi_term-0.11.0 \
		atk-sys-0.7.0 \
		atty-0.2.13 \
		bitflags-1.0.4 \
		cairo-rs-0.5.0 \
		cairo-sys-rs-0.7.0 \
		cc-1.0.45 \
		clap-2.32.0 \
		dtoa-0.4.4 \
		fragile-0.3.0 \
		gdk-0.9.0 \
		gdk-pixbuf-0.5.0 \
		gdk-pixbuf-sys-0.7.0 \
		gdk-sys-0.7.0 \
		gio-0.5.1 \
		gio-sys-0.7.0 \
		glib-0.6.1 \
		glib-sys-0.7.0 \
		gobject-sys-0.7.0 \
		gtk-0.5.0 \
		gtk-sys-0.7.0 \
		lazy_static-1.4.0 \
		libc-0.2.62 \
		linked-hash-map-0.5.2 \
		maplit-1.0.2 \
		memchr-2.2.1 \
		memmap-0.7.0 \
		pango-0.5.0 \
		pango-sys-0.7.0 \
		pkg-config-0.3.16 \
		proc-macro2-1.0.4 \
		quote-1.0.2 \
		regex-1.1.9 \
		regex-syntax-0.6.12 \
		serde-1.0.101 \
		serde_derive-1.0.101 \
		serde_yaml-0.8.9 \
		strsim-0.7.0 \
		syn-1.0.5 \
		textwrap-0.10.0 \
		thread_local-0.3.6 \
		unicode-width-0.1.7 \
		unicode-xid-0.2.0 \
		utf8-ranges-1.0.4 \
		vec_map-0.8.1 \
		winapi-0.3.8 \
		winapi-i686-pc-windows-gnu-0.4.0 \
		winapi-x86_64-pc-windows-gnu-0.4.0 \
		xkbcommon-0.4.0 \
		yaml-rust-0.4.3
CARGO_BUILD=	no
CARGO_INSTALL=	no
CARGO_TEST=	no

post-patch:
# Add --verbose after each cargo subcommand
# Don't use BSD realpath(1) against non-existing files
	@${REINPLACE_CMD} -e '/^cargo/ { \
		  s,^,cmd=$$1; shift; ,; \
		  s,"$$@","$$cmd" --verbose &,; }' \
		-e '/OUT_PATH=/s,=.*,=$$PWD/$$1,' \
		${WRKSRC}/cargo*.sh

.include <bsd.port.mk>
