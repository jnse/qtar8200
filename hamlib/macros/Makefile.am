## Please update this variable if any new macros are created

MACROS = \
	aclocal-include.m4 \
	acx_pthread.m4 \
	lf_warnings.m4 \
	gr_doxygen.m4 \
	gr_pwin32.m4 \
	gr_swig.m4 \
	hl_getaddrinfo.m4 \
	perl.m4 \
	ac_python_devel.m4 \
	tcl.m4


EXTRA_DIST=$(MACROS)
MAINTAINERCLEANFILES=macros.dep

@MAINT@macros.dep: Makefile.am
@MAINT@ @echo '$$(top_srcdir)/aclocal.m4: $(MACROS:%=macros/%)' > $@

