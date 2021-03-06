#
# This file and its contents are supplied under the terms of the
# Common Development and Distribution License ("CDDL"), version 1.0.
# You may only use this file in accordance with the terms of version
# 1.0 of the CDDL.
#
# A full copy of the text of the CDDL should have accompanied this
# source.  A copy of the CDDL is also available via the Internet at
# http://www.illumos.org/license/CDDL.
#

#
# Copyright (c) 2018, Joyent, Inc.
#

UTSBASE = ../..

MODULE		= i40e
OBJECTS		= $(I40E_OBJS:%=$(OBJS_DIR)/%) $(I40E_INTC_OBJS:%=$(OBJS_DIR)/%)
LINTS		= $(I40E_OBJS:%.o=$(LINTS_DIR)/%.ln)
ROOTMODULE	= $(ROOT_DRV_DIR)/$(MODULE)
CONF_SRCDIR	= $(UTSBASE)/common/io/i40e

include $(UTSBASE)/intel/Makefile.intel

CPPFLAGS	+= -I$(UTSBASE)/common/io/i40e
CPPFLAGS	+= -I$(UTSBASE)/common/io/i40e/core

ALL_TARGET	= $(BINARY) $(CONFMOD)
LINT_TARGET	= $(MODULE).lint
INSTALL_TARGET	= $(BINARY) $(ROOTMODULE) $(ROOT_CONFFILE)

#
# The Intel common code defines some values in header files that end up in all
# of our objects. Therefore we don't try to lint for that.
#
LINTTAGS	+= -erroff=E_STATIC_UNUSED
LINTTAGS	+= -erroff=E_ENUM_VAL_OVERFLOWS_INT_MAX

#
# The Intel common code defines some enums which are valid unsigned ints that
# GCC is fine with, but not Studio.
#
CERRWARN   += -_cc=-erroff=E_ENUM_VAL_OVERFLOWS_INT_MAX

# 3rd party code
SMOFF += all_func_returns

LDFLAGS		+= -dy -N misc/mac

MAPFILES	+= ddi mac random

.KEEP_STATE:

def:		$(DEF_DEPS)

all:		$(ALL_DEPS)

clean:		$(CLEAN_DEPS)

clobber:	$(CLOBBER_DEPS)

lint:		$(LINT_DEPS)

modlintlib:	$(MODLINTLIB_DEPS)

clean.lint:	$(CLEAN_LINT_DEPS)

install:	$(INSTALL_DEPS)

include $(UTSBASE)/Makefile.mapfile
include $(UTSBASE)/intel/Makefile.targ
