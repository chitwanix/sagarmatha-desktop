CLEANFILES =

noinst_LTLIBRARIES =
lib_LTLIBRARIES = libsagarmatha-desktop.la

AM_CPPFLAGS =							\
	-I$(top_srcdir)						\
	-I$(srcdir)/libgsystem					\
	$(SAGARMATHA_DESKTOP_CFLAGS)					\
	$(XLIB_CFLAGS)						\
	-DG_LOG_DOMAIN=\"SagarmathaDesktop\"				\
	-DGNOMELOCALEDIR=\""$(prefix)/$(DATADIRNAME)/locale\""	\
	-DPNP_IDS=\""$(PNP_IDS)"\"				\
	-DXKB_BASE=\""$(XKB_BASE)"\"				\
	$(DISABLE_DEPRECATED_CFLAGS)

AM_CFLAGS = $(WARN_CFLAGS)

libgsystem_srcpath := libgsystem
libgsystem_cflags = $(SAGARMATHA_DESKTOP_CFLAGS)
libgsystem_libs = $(SAGARMATHA_DESKTOP_LIBS)
include libgsystem/Makefile-libgsystem.am

introspection_sources = 		\
	gnome-desktop-utils.c		\
	gnome-desktop-thumbnail.c 	\
	gnome-thumbnail-pixbuf-utils.c 	\
	gnome-bg.c			\
	gnome-bg-crossfade.c		\
	display-name.c			\
	gnome-rr.c			\
	gnome-rr-config.c		\
	gnome-rr-output-info.c		\
	gnome-rr-labeler.c		\
	gnome-pnp-ids.c			\
	gnome-wall-clock.c		\
	gnome-xkb-info.c		\
	edid-parse.c

libsagarmatha_desktop_la_SOURCES = 	\
	$(introspection_sources)	\
	gnome-datetime-source.h		\
	gnome-datetime-source.c		\
	gnome-rr-private.h		\
	edid.h				\
	private.h

libsagarmatha_desktop_la_LIBADD =	\
	$(XLIB_LIBS)		\
	$(LIBM)			\
	$(SAGARMATHA_DESKTOP_LIBS)	\
	libgsystem.la           \
	-lrt

libsagarmatha_desktop_la_LDFLAGS = \
	-version-info $(LT_VERSION) \
	-export-symbols-regex "^gnome_.*" \
	-no-undefined

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = sagarmatha-desktop.pc

libsagarmatha_desktopdir = $(includedir)/sagarmatha-desktop/libsagarmatha-desktop
libsagarmatha_desktop_HEADERS = \
        gnome-bg.h                      \
        gnome-bg-crossfade.h            \
        gnome-desktop-utils.h           \
        gnome-desktop-thumbnail.h       \
        gnome-rr.h                      \
        gnome-rr-config.h               \
        gnome-rr-labeler.h		\
        gnome-pnp-ids.h			\
        gnome-wall-clock.h		\
	gnome-xkb-info.h		\
	cdesktop-enums.h

if USE_INTERNAL_PNP_IDS
pnpdatadir = $(datadir)/libsagarmatha-desktop
pnpdata_DATA = pnp.ids
endif
pnpdata_DATA_dist = pnp.ids

check:
	test -s $(top_srcdir)/libsagarmatha-desktop/pnp.ids

-include $(INTROSPECTION_MAKEFILE)
INTROSPECTION_GIRS =
INTROSPECTION_SCANNER_ARGS = --add-include-path=$(srcdir) --warn-all
INTROSPECTION_COMPILER_ARGS = --includedir=$(srcdir)

if HAVE_INTROSPECTION


CDesktopEnums_3_0_gir_CFLAGS = -I$(srcdir)
CDesktopEnums_3_0_gir_FILES = cdesktop-enums.h
CDesktopEnums_3_0_gir_SCANNERFLAGS = --header-only --identifier-prefix=CDesktop
INTROSPECTION_GIRS += CDesktopEnums-3.0.gir
SagarmathaDesktop-3.0.gir: libsagarmatha-desktop.la
SagarmathaDesktop_3_0_gir_INCLUDES = GObject-2.0 Gtk-3.0
SagarmathaDesktop_3_0_gir_PACKAGES = gdk-pixbuf-2.0 glib-2.0 gobject-2.0 gio-2.0 gtk+-3.0
SagarmathaDesktop_3_0_gir_EXPORT_PACKAGES = sagarmatha-desktop
SagarmathaDesktop_3_0_gir_CFLAGS = -DGNOME_DESKTOP_USE_UNSTABLE_API -I$(top_srcdir)
SagarmathaDesktop_3_0_gir_LIBS = libsagarmatha-desktop.la
SagarmathaDesktop_3_0_gir_FILES = $(introspection_sources) $(libsagarmatha_desktop_HEADERS)
SagarmathaDesktop_3_0_gir_SCANNERFLAGS = --identifier-prefix=Gnome --symbol-prefix=gnome_
INTROSPECTION_SCANNER_ARGS += $(patsubst %,--c-include='libsagarmatha-desktop/%',$(libsagarmatha_desktop_HEADERS))
INTROSPECTION_GIRS += SagarmathaDesktop-3.0.gir

girdir = $(datadir)/gir-1.0
gir_DATA = $(INTROSPECTION_GIRS)

typelibdir = $(libdir)/girepository-1.0
typelib_DATA = $(INTROSPECTION_GIRS:.gir=.typelib)

CLEANFILES += $(gir_DATA) $(typelib_DATA)
endif

EXTRA_DIST = \
	sagarmatha-desktop.pc.in			\
	sagarmatha-desktop-uninstalled.pc.in	\
	$(pnpdata_DATA_dist)

MAINTAINERCLEANFILES = \
	pnp.ids

libexec_PROGRAMS =		\
	sagarmatha-rr-debug

sagarmatha_rr_debug_SOURCES =	\
	sagarmatha-rr-debug.c

sagarmatha_rr_debug_LDADD =		\
	$(SAGARMATHA_DESKTOP_LIBS)	\
	$(lib_LTLIBRARIES)	\
	$(XLIB_LIBS)

noinst_PROGRAMS = test-xkb-info test-pnp-ids test-wall-clock
test_xkb_info_LDADD =		\
	$(SAGARMATHA_DESKTOP_LIBS)	\
	$(lib_LTLIBRARIES)	\
	$(XLIB_LIBS)

test_pnp_ids_LDADD = $(test_xkb_info_LDADD)

test_wall_clock_LDADD = $(test_xkb_info_LDADD)

-include $(top_srcdir)/git.mk
