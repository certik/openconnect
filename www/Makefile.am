#

SUBDIRS = styles inc images
CONV 	= "$(srcdir)/html.py"

FTR_PAGES = csd.html features.html gui.html nonroot.html
START_PAGES = building.html connecting.html manual.html vpnc-script.html 
INDEX_PAGES = changelog.html download.html index.html packages.html platforms.html
TOPLEVEL_PAGES = contribute.html mail.html technical.html

ALL_PAGES = $(FTR_PAGES) $(START_PAGES) $(INDEX_PAGES) $(TOPLEVEL_PAGES)

html_DATA = $(ALL_PAGES)

.xml.html:
	$(PYTHON) $(CONV) -d $(srcdir) $< > $@ || (rm $@; exit 1)

clean-local:
	rm -f $(ALL_PAGES) openconnect.8.inc

$(ALL_PAGES): menu1.xml $(srcdir)/inc/*.tmpl
$(FTR_PAGES): menu2-features.xml
$(START_PAGES): menu2-started.xml
$(MAIN_PAGES): menu2.xml

manual.html: openconnect.8.inc

$(top_builddir)/openconnect.8: $(top_srcdir)/openconnect.8.in $(top_builddir)/config.status
	cd $(top_builddir) && $(SHELL) ./config.status openconnect.8

openconnect.8.inc: $(top_builddir)/openconnect.8
	groff -t -K UTF-8 -mandoc -Txhtml $? | sed -e '1,/<body>/d' -e '/<\/body>/,$$d' > $@

EXTRA_DIST = $(patsubst %.html,%.xml,$(ALL_PAGES)) $(srcdir)/menu1.xml $(srcdir)/menu2*.xml $(srcdir)/html.py
