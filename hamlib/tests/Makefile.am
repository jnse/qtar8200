# Current Autotools documentation suggests that DejaGNU is obsolete
# and replaced by Autotest.  TODO: implement Autotest

# AUTOMAKE_OPTIONS = dejagnu
# DEJATOOL = testfreq testbcd testloc rigctl

DISTCLEANFILES = rigctl.log rigctl.sum testbcd.log testbcd.sum

bin_PROGRAMS = rigctl rigmem rigswr rigsmtr rotctl rigctld rotctld
man_MANS = rigctl.1 rigmem.1 rigswr.1 rigsmtr.1 rotctl.1 rigctld.8 rotctld.8

check_PROGRAMS = dumpmem testrig testtrn testbcd testfreq listrigs \
		 testloc rig_bench @RIGMATRIX@

rigctl_SOURCES = rigctl.c rigctl_parse.c dumpcaps.c sprintflst.c
rigctld_SOURCES = rigctld.c rigctl_parse.c dumpcaps.c sprintflst.c
rotctl_SOURCES = rotctl.c rotctl_parse.c dumpcaps_rot.c
rotctld_SOURCES = rotctld.c rotctl_parse.c dumpcaps_rot.c
rigswr_SOURCES = rigswr.c
rigsmtr_SOURCES = rigsmtr.c
rigmem_SOURCES = rigmem.c memsave.c memload.c memcsv.c sprintflst.c
noinst_HEADERS = sprintflst.h rigctl_parse.h rotctl_parse.h

EXTRA_PROGRAMS = rigmatrix rigctld rotctld

# all the programs need this
LDADD = $(top_builddir)/src/libhamlib.la $(top_builddir)/lib/libmisc.la
DEPENDENCIES = $(top_builddir)/src/libhamlib.la

rigmem_CFLAGS = $(AM_CFLAGS) @LIBXML2_CFLAGS@

## Linker options
listrigs_LDFLAGS = @BACKENDLNK@
dumpmem_LDFLAGS = @BACKENDLNK@
testrig_LDFLAGS = @BACKENDLNK@
rig_bench_LDFLAGS = $(top_builddir)/lib/libmisc.la @BACKENDLNK@
testtrn_LDFLAGS = @BACKENDLNK@
rigctl_LDFLAGS = @BACKENDLNK@
rigswr_LDFLAGS = @BACKENDLNK@
rigsmtr_LDFLAGS = @BACKENDLNK@
rigmem_LDFLAGS = @BACKENDLNK@ @LIBXML2_LIBS@
rotctl_LDFLAGS = @ROT_BACKENDLNK@
rigctld_LDFLAGS = @BACKENDLNK@ @PTHREAD_LIBS@ @NET_LIBS@
rotctld_LDFLAGS = @ROT_BACKENDLNK@ @PTHREAD_LIBS@ @NET_LIBS@

# temporary hack
testbcd_LDFLAGS = -dlpreopen self
testloc_LDFLAGS = -dlpreopen self

# rigmatrix needs also libgd
rigmatrix_LDFLAGS = -lgd -lz @BACKENDLNK@

## Dependencies

dumpmem_DEPENDENCIES = $(DEPENDENCIES) @BACKENDEPS@
testrig_DEPENDENCIES = $(DEPENDENCIES) @BACKENDEPS@
rig_bench_DEPENDENCIES = $(DEPENDENCIES) @BACKENDEPS@
testtrn_DEPENDENCIES = $(DEPENDENCIES) @BACKENDEPS@
listrigs_DEPENDENCIES = $(DEPENDENCIES) @BACKENDEPS@
rigctl_DEPENDENCIES = $(DEPENDENCIES) @BACKENDEPS@
rigmem_DEPENDENCIES = $(DEPENDENCIES) @BACKENDEPS@
rigswr_DEPENDENCIES = $(DEPENDENCIES) @BACKENDEPS@
rigsmtr_DEPENDENCIES = $(DEPENDENCIES) @BACKENDEPS@
rotctl_DEPENDENCIES = $(DEPENDENCIES) @ROT_BACKENDEPS@
rigmatrix_DEPENDENCIES = $(DEPENDENCIES) @BACKENDEPS@
rigctld_DEPENDENCIES = $(DEPENDENCIES) @BACKENDEPS@
rotctld_DEPENDENCIES = $(DEPENDENCIES) @ROT_BACKENDEPS@



rigmatrix.html: rigmatrix_head.html rigmatrix listrigs
	mkdir -p sup-info/support
	( cat $(srcdir)/rigmatrix_head.html && cd sup-info && ../rigmatrix ) > sup-info/rigmatrix.html
	for f in `./listrigs | tail -n +2 | cut -f1` ; do ( ./rigctl -m $$f -u > sup-info/support/model$$f.txt || exit 0 ) ; done
	./rigctl -l |sort -n | $(srcdir)/rig_split_lst.awk -v lst_dir="sup-info"

EXTRA_DIST = rigmatrix_head.html rig_split_lst.awk $(man_MANS) testctld.pl testrotctld.pl

# Support 'make check' target for simple tests
check_SCRIPTS = testrig.sh testfreq.sh testbcd.sh testloc.sh

TESTS = $(check_SCRIPTS)


testrig.sh:
	echo './testrig 1' > testrig.sh
	chmod +x ./testrig.sh

testfreq.sh:
	echo './testfreq' > testfreq.sh
	chmod +x ./testfreq.sh

testbcd.sh:
	echo './testbcd 146520000 10' > testbcd.sh
	chmod +x ./testbcd.sh

testloc.sh:
	echo './testloc EM79UT96LW 5' > testloc.sh
	chmod +x ./testloc.sh


CLEANFILES = testrig.sh testfreq.sh testbcd.sh testloc.sh

