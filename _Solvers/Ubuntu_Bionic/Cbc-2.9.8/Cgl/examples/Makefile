# Copyright (C) 2006 International Business Machines and others.
# All Rights Reserved.
# This file is distributed under the Eclipse Public License.

# $Id: Makefile.in 726 2006-04-17 04:16:00Z andreasw $

##########################################################################
#    You can modify this example makefile to fit for your own program.   #
#    Usually, you only need to change the five CHANGEME entries below.   #
##########################################################################

# To compile other examples, either changed the following line, or
# add the argument DRIVER=filename_without_extension to make
DRIVER = cgl1

# CHANGEME: This should be the name of your executable
EXE = $(DRIVER)

# CHANGEME: Here is the name of all object files corresponding to the source
#           code that you wrote in order to define the problem statement
OBJS =  $(DRIVER).o

# CHANGEME: Additional libraries
ADDLIBS =

# CHANGEME: Additional flags for compilation (e.g., include flags)
ADDINCFLAGS =

# CHANGEME: Directory to the sources for the (example) problem definition
# files
SRCDIR = .


##########################################################################
#  Usually, you don't have to change anything below.  Note that if you   #
#  change certain compiler options, you might have to recompile the      #
#  package.                                                              #
##########################################################################

COIN_HAS_PKGCONFIG = #TRUE
COIN_CXX_IS_CL = #TRUE
COIN_HAS_SAMPLE = TRUE

# C++ Compiler command
CXX = g++

# C++ Compiler options
CXXFLAGS = -O3 -pipe -DNDEBUG -pedantic-errors -Wparentheses -Wreturn-type -Wcast-qual -Wall -Wpointer-arith -Wwrite-strings -Wconversion -Wno-unknown-pragmas -Wno-long-long   -DCGL_BUILD

# additional C++ Compiler options for linking
CXXLINKFLAGS =  -Wl,--rpath -Wl,/home/mf/Cbc-2.9.8/lib

# Sample data directory
ifeq ($(COIN_HAS_SAMPLE), TRUE)
  ifeq ($(COIN_HAS_PKGCONFIG), TRUE)
    CXXFLAGS += -DSAMPLEDIR=\"`PKG_CONFIG_PATH=/home/mf/Cbc-2.9.8/lib64/pkgconfig:/home/mf/Cbc-2.9.8/lib/pkgconfig:/home/mf/Cbc-2.9.8/share/pkgconfig:  --variable=datadir coindatasample`\"
  else
    CXXFLAGS += -DSAMPLEDIR=\"/home/mf/Cbc-2.9.8/share/coin/Data/Sample\"
  endif
endif

# Include directories (we use the CYGPATH_W variables to allow compilation with Windows compilers)
ifeq ($(COIN_HAS_PKGCONFIG), TRUE)
  INCL = `PKG_CONFIG_PATH=/home/mf/Cbc-2.9.8/lib64/pkgconfig:/home/mf/Cbc-2.9.8/lib/pkgconfig:/home/mf/Cbc-2.9.8/share/pkgconfig:  --cflags cgl`
else
  INCL =  -I/home/mf/Cbc-2.9.8/include/coin  -I/home/mf/Cbc-2.9.8/include/coin  -I/home/mf/Cbc-2.9.8/include/coin  -I/home/mf/Cbc-2.9.8/include/coin   -I/home/mf/Cbc-2.9.8/include/coin  -I/home/mf/Cbc-2.9.8/include/coin   -I/home/mf/Cbc-2.9.8/include/coin  
endif
INCL += $(ADDINCFLAGS)

# Linker flags
ifeq ($(COIN_HAS_PKGCONFIG), TRUE)
  LIBS = `PKG_CONFIG_PATH=/home/mf/Cbc-2.9.8/lib64/pkgconfig:/home/mf/Cbc-2.9.8/lib/pkgconfig:/home/mf/Cbc-2.9.8/share/pkgconfig:  --libs cgl`
else
  ifeq ($(COIN_CXX_IS_CL), TRUE)
    LIBS = -link -libpath:`$(CYGPATH_W) /home/mf/Cbc-2.9.8/lib` libCgl.lib  -L/home/mf/Cbc-2.9.8/lib -lOsiClp   -L/home/mf/Cbc-2.9.8/lib -lClpSolver -lClp   -L/home/mf/Cbc-2.9.8/lib -lOsi   -L/home/mf/Cbc-2.9.8/lib -lCoinUtils -lm    -L/home/mf/Cbc-2.9.8/lib -lOsi   -L/home/mf/Cbc-2.9.8/lib -lCoinUtils -lm    -L/home/mf/Cbc-2.9.8/lib -lCoinUtils -lm   
  else
    LIBS = -L/home/mf/Cbc-2.9.8/lib -lCgl  -L/home/mf/Cbc-2.9.8/lib -lOsiClp   -L/home/mf/Cbc-2.9.8/lib -lClpSolver -lClp   -L/home/mf/Cbc-2.9.8/lib -lOsi   -L/home/mf/Cbc-2.9.8/lib -lCoinUtils -lm    -L/home/mf/Cbc-2.9.8/lib -lOsi   -L/home/mf/Cbc-2.9.8/lib -lCoinUtils -lm    -L/home/mf/Cbc-2.9.8/lib -lCoinUtils -lm   
  endif
endif

# The following is necessary under cygwin, if native compilers are used
CYGPATH_W = echo

all: $(EXE)

.SUFFIXES: .cpp .c .o .obj

$(EXE): $(OBJS)
	bla=;\
	for file in $(OBJS); do bla="$$bla `$(CYGPATH_W) $$file`"; done; \
	$(CXX) $(CXXLINKFLAGS) $(CXXFLAGS) -o $@ $$bla $(ADDLIBS) $(LIBS)

clean:
	rm -rf $(EXE) $(OBJS)

.cpp.o:
	$(CXX) $(CXXFLAGS) $(INCL) -c -o $@ `test -f '$<' || echo '$(SRCDIR)/'`$<


.cpp.obj:
	$(CXX) $(CXXFLAGS) $(INCL) -c -o $@ `if test -f '$<'; then $(CYGPATH_W) '$<'; else $(CYGPATH_W) '$(SRCDIR)/$<'; fi`

.c.o:
	$(CC) $(CFLAGS) $(INCL) -c -o $@ `test -f '$<' || echo '$(SRCDIR)/'`$<


.c.obj:
	$(CC) $(CFLAGS) $(INCL) -c -o $@ `if test -f '$<'; then $(CYGPATH_W) '$<'; else $(CYGPATH_W) '$(SRCDIR)/$<'; fi`
