COLM_BIN    = ../../colm/colm
COLM_WRAP   = ../../colm/colm-wrap
COLM_LA     = ../../colm/libcolm.la
COLM_LIBDEP = $(COLM_LA)
COLM_BINDEP = $(COLM_BIN) $(COLM_WRAP)

bin_PROGRAMS = ragel-ruby

ragel_ruby_CPPFLAGS = -I$(top_srcdir)/aapl -I$(top_srcdir)/ragel -I$(top_srcdir)/colm/include

dist_ragel_ruby_SOURCES = main.cc rlhc.c

nodist_ragel_ruby_SOURCES = \
	rlparse.c rlreduce.cc

ragel_ruby_LDADD = ../libragel.la ../libfsm.la $(COLM_LA)

BUILT_SOURCES = rlparse.c rlreduce.cc rlhc.c

EXTRA_DIST = rlparse.lm rlhc.lm

rlparse.pack: rlparse.lm $(COLM_BINDEP)
	$(COLM_WRAP) -c -I .. -b rlparseRuby -o $@ -p rlparse.c -m rlreduce.cc $<

rlparse.c: rlparse.pack
	$(COLM_WRAP) -o $@ $<

rlreduce.cc: rlparse.pack
	$(COLM_WRAP) -o $@ $<

rlhc.c: rlhc.lm ../ril.lm $(COLM_BINDEP)
	$(COLM_BIN) -c -I .. -b rlhcRuby -o $@ $<
