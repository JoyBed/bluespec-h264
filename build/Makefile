#=======================================================================
# 6.375 Makefile for bsc-compile
#-----------------------------------------------------------------------
# $Id: Makefile,v 1.14 2008-06-26 18:12:03 jamey.hicks Exp $
#

basedir  = ..

#--------------------------------------------------------------------
# Sources
#--------------------------------------------------------------------


# Bluespec sources

toplevel_module = mkTH

srcdir = $(basedir)/src
reldir = $(basedir)/release
lcpdir = $(basedir)/LumaChromaParallel

#--------------------------------------------------------------------
# Build rules
#--------------------------------------------------------------------

BSC_COMP = bsc
#BSC_OPTS = -u -show-module-use -verilog -keep-fires -aggressive-conditions \
#           -relax-method-earliness -relax-method-urgency -v

VER_OPTS =  +RTS -K100000000 --RTS -u -v -verilog -aggressive-conditions
SIM_OPTS =  +RTS -K100000000 --RTS -u -v -sim -aggressive-conditions -show-schedule
BDIR ?= build
#--------------------------------------------------------------------
# Default make target
#--------------------------------------------------------------------

# all : mainline
all : release

$(BDIR):
	mkdir -p $@

mainline: $(BDIR)
	$(BSC_COMP) $(SIM_OPTS) -bdir $(BDIR) -p +:$(srcdir) -g $(toplevel_module) $(srcdir)/$(toplevel_module).bsv > out.log

release: $(BDIR)
	$(BSC_COMP) $(SIM_OPTS) -bdir $(BDIR) -p +:$(reldir) -g $(toplevel_module) $(reldir)/$(toplevel_module).bsv > out.log

LCP: $(BDIR)
	$(BSC_COMP) $(SIM_OPTS) -bdir $(BDIR) -p +:$(lcpdir):$(reldir) -g $(toplevel_module) $(lcpdir)/$(toplevel_module).bsv > out.log

mainline_verilog: $(BDIR)
	$(BSC_COMP) $(VER_OPTS) -bdir $(BDIR) -p +:$(srcdir) -g $(toplevel_module) $(srcdir)/$(toplevel_module).bsv > out.log

release_verilog: $(BDIR)
	$(BSC_COMP) $(VER_OPTS) -bdir $(BDIR) -p +:$(reldir) -g $(toplevel_module) $(reldir)/$(toplevel_module).bsv > out.log

LCP_verilog: $(BDIR)
	$(BSC_COMP) $(VER_OPTS) -bdir $(BDIR) -p +:$(lcpdir):$(reldir) -g $(toplevel_module) $(lcpdir)/$(toplevel_module).bsv > out.log


#--------------------------------------------------------------------
# Clean up
#--------------------------------------------------------------------
clean:
	rm -rf $(junk) *~ \#* *.cxx *.ba *.o *.h *.bi *.bo *.bsv *.log $(BDIR)
