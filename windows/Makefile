include ../py/mkenv.mk
-include mpconfigport.mk

# define main target
PROG = micropython.exe

# qstr definitions (must come before including py.mk)
QSTR_DEFS = ../unix/qstrdefsport.h

# include py core make definitions
include ../py/py.mk

INC =  -I.
INC += -I..
INC += -I$(BUILD)

# compiler settings
CFLAGS = $(INC) -Wall -Wpointer-arith -Werror -ansi -std=gnu99 -DUNIX -D__USE_MINGW_ANSI_STDIO=1 $(CFLAGS_MOD) $(COPT)
LDFLAGS = $(LDFLAGS_MOD) -lm

# Debugging/Optimization
ifdef DEBUG
CFLAGS += -g
COPT = -O0
else
COPT = -Os #-DNDEBUG
endif

# source files
SRC_C = \
	unix/main.c \
	unix/file.c \
	unix/input.c \
	unix/unix_mphal.c \
	unix/modos.c \
	unix/modtime.c \
	unix/gccollect.c \
	realpath.c \
	init.c \
	sleep.c \

OBJ = $(PY_O) $(addprefix $(BUILD)/, $(SRC_C:.c=.o))

ifeq ($(MICROPY_USE_READLINE),1)
CFLAGS_MOD += -DMICROPY_USE_READLINE=1
LDFLAGS_MOD += -lreadline
# the following is needed for BSD
#LDFLAGS_MOD += -ltermcap
endif

LIB += -lws2_32
#LIB += -lmman

include ../py/mkrules.mk

