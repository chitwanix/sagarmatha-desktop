desktop_gschemas_in_in =						\
	org.sagarmatha.desktop.default-applications.gschema.xml.in.in	\
	org.sagarmatha.desktop.interface.gschema.xml.in.in			\
	org.sagarmatha.desktop.lockdown.gschema.xml.in.in			\
	org.sagarmatha.system.locale.gschema.xml.in.in			\
	org.sagarmatha.desktop.sound.gschema.xml.in.in			\
	org.sagarmatha.desktop.thumbnail-cache.gschema.xml.in.in		\
	org.sagarmatha.desktop.a11y.keyboard.gschema.xml.in.in		\
	org.sagarmatha.desktop.a11y.applications.gschema.xml.in.in		\
	org.sagarmatha.desktop.a11y.magnifier.gschema.xml.in.in		\
	org.sagarmatha.desktop.a11y.mouse.gschema.xml.in.in			\
	org.sagarmatha.desktop.thumbnailers.gschema.xml.in.in		\
	org.sagarmatha.desktop.session.gschema.xml.in.in			\
	org.sagarmatha.desktop.background.gschema.xml.in.in			\
	org.sagarmatha.desktop.media-handling.gschema.xml.in.in		\
	org.sagarmatha.desktop.screensaver.gschema.xml.in.in			\
	org.sagarmatha.desktop.wm.preferences.gschema.xml.in.in		\
	org.sagarmatha.desktop.input-sources.gschema.xml.in.in

@INTLTOOL_XML_NOMERGE_RULE@

gsettings_ENUM_NAMESPACE = org.sagarmatha.desktop
gsettings_ENUM_FILES = $(top_srcdir)/libsagarmatha-desktop/*.h

desktop_gschemas_in = $(desktop_gschemas_in_in:.xml.in.in=.xml.in)
gsettings_SCHEMAS = $(desktop_gschemas_in:.xml.in=.xml)

%.gschema.xml.in: %.gschema.xml.in.in Makefile
	$(AM_V_GEN) $(SED) -e 's^\@datadir\@^$(datadir)^g' -e 's^\@GETTEXT_PACKAGE\@^$(GETTEXT_PACKAGE)^g' < $< > $@

@GSETTINGS_RULES@

EXTRA_DIST =				\
	$(desktop_gschemas_in_in)

CLEANFILES =					\
	$(gsettings__enum_file)			\
	$(gsettings_SCHEMAS)			\
	$(desktop_gschemas_in)			\
	*.gschema.valid

-include $(top_srcdir)/git.mk
