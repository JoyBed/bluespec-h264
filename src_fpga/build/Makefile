#=======================================================================
# 6.375 Makefile for bsc-compile
#-----------------------------------------------------------------------
# $Id: Makefile,v 1.3 2008-06-26 17:52:59 jamey.hicks Exp $
#

default : all

BDIR ?= build

#--------------------------------------------------------------------
# Sources location
#--------------------------------------------------------------------
basedir  = ..

# Bluespec sources
toplevel_module = mkTestBench
srcdir = $(basedir)

#--------------------------------------------------------------------
# Build rules
#--------------------------------------------------------------------
BSC_COMP = bsc
#BSC_OPTS = -u -show-module-use - -keep-fires -aggressive-conditions \
#           -relax-method-earliness -relax-method-urgency -v

VER_OPTS = +RTS -K100000000 --RTS -u -v -verilog -aggressive-conditions
SIM_OPTS = +RTS -K100000000 --RTS -u -v -sim -aggressive-conditions

# Run the bluespec compiler
bsv_TH_vsrc = $(toplevel_module).v
$(bsv_TH_vsrc): $(BDIR)
	$(BSC_COMP) $(VER_OPTS) -bdir $(BDIR) -p +:$(basedir) -g $(toplevel_module) $(basedir)/$(toplevel_module).bsv > out.log

compile : $(BDIR) $(toplevel_module).v

$(BDIR):
	mkdir -p $@

# Create a schedule file
schedule_rpt = schedule.rpt
$(schedule_rpt): $(BDIR)
	$(BSC_COMP) $(VER_OPTS) -show-schedule -show-rule-rel \* \* -bdir $(BDIR) -p +:$(basedir) -g $(toplevel_module) \
                $(basedir)/$(toplevel_module).bsv >& $(schedule_rpt)

#--------------------------------------------------------------------
# Default make target
#--------------------------------------------------------------------

all : compile
#--------------------------------------------------------------------
# Clean up
#--------------------------------------------------------------------

clean :
	rm -rf $(schedule_rpt) *.log $(BDIR)
