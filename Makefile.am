## Process this file with automake to produce Makefile.in

AM_CPPFLAGS = $(GTK_CFLAGS)
usbview_LDADD = $(GTK_LIBS)

bin_PROGRAMS = usbview

man_MANS = usbview.8

usbview_SOURCES =		\
	main.c			\
	interface.c		\
	callbacks.c		\
	usbtree.c usbtree.h	\
	usbparse.c usbparse.h	\
	configure-dialog.c      \
	usbview_logo.xpm

interface.o: $(icon_bitmaps_xpm)

EXTRA_DIST = $(man_MANS) usbview_icon.svg usbview.desktop usbview.spec usbview_logo.xcf

desktopdir = $(datadir)/applications
if DESKTOP
desktop_DATA = usbview.desktop
endif

icondir = $(datadir)/icons

icon_bitmaps_png = \
       hicolor/16x16/apps/usbview.png \
       hicolor/22x22/apps/usbview.png \
       hicolor/32x32/apps/usbview.png \
       hicolor/48x48/apps/usbview.png \
       hicolor/64x64/apps/usbview.png \
       hicolor/256x256/apps/usbview.png

icon_bitmaps_xpm = hicolor/64x64/apps/usbview_icon.xpm

if ICONS
nobase_icon_DATA = $(icon_scalable) $(icon_bitmaps_png)
endif

$(icon_bitmaps_png): usbview_icon.svg
	mkdir -p $$(dirname $@)
if USE_INKSCAPE
	$(INKSCAPE) --export-png=$@ --export-width=$$(basename $$(dirname $$(dirname $@))) $<
else
if USE_CONVERT
	$(CONVERT) -geometry $$(basename $$(dirname $$(dirname $@))) $< $@
else
	echo "error: unable to generate $@ from $<"
	exit 1
endif
endif

$(icon_bitmaps_xpm): usbview_icon.svg
	mkdir -p $$(dirname $@)
if HAVE_CONVERT
	$(CONVERT) -geometry $$(basename $$(dirname $$(dirname $@))) $< $@
else
	echo "error: unable to generate $@ from $<"
	exit 1
endif

icon_scalable = hicolor/scalable/apps/usbview.svg

$(icon_scalable): usbview_icon.svg
	mkdir -p $$(dirname $@)
	cp $< $@

CLEANFILES = $(icon_scalable) $(icon_bitmaps_png) $(icon_bitmaps_xpm)

# gtk_update_icon_cache = gtk-update-icon-cache -f -t $(datadir)/icons/hicolor; gtk-update-icon-cache -f -t $(datadir)/icons/HighContrast
#
# install-data-hook: update-icon-cache
# uninstall-hook: update-icon-cache
# update-icon-cache:
#	@-if test -z "$(DESTDIR)"; then \
#		echo "Updating Gtk icon cache."; \
#		$(gtk_update_icon_cache); \
#	else \
#		echo "*** Icon cache not updated.  After (un)install, run this:"; \
#		echo "***   $(gtk_update_icon_cache)"; \
#	fi
