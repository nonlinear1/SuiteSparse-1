#-------------------------------------------------------------------------------
# COLAMD Lib/Makefile
#-------------------------------------------------------------------------------

LIBRARY = libcolamd
VERSION = 2.9.6
SO_VERSION = 2

default: library

include ../../SuiteSparse_config/SuiteSparse_config.mk

# COLAMD depends on SuiteSparse_config
LDLIBS += -lsuitesparseconfig

# compile and install in SuiteSparse/lib
library:
	$(MAKE) install INSTALL=$(SUITESPARSE)

I = -I../Include -I../../SuiteSparse_config

INC = ../Include/colamd.h ../../SuiteSparse_config/SuiteSparse_config.h

SRC = ../Source/colamd.c

OBJ = colamd.o colamd_l.o

colamd.o: $(SRC) $(INC)
	$(CC) $(CF) $(I) -c ../Source/colamd.c

colamd_l.o: $(SRC) $(INC)
	$(CC) $(CF) $(I) -c ../Source/colamd.c -DDLONG -o colamd_l.o

# creates libcolamd.a, a C-callable COLAMD library
static: $(AR_TARGET)

$(AR_TARGET):  $(OBJ)
	$(ARCHIVE)  $@ $^
	- $(RANLIB) $@ 

ccode: library

clean:
	- $(RM) -r $(CLEAN)

purge: distclean

distclean: clean
	- $(RM) -r $(PURGE)

# install COLAMD
install: $(AR_TARGET) $(INSTALL_LIB)/$(SO_TARGET)

$(INSTALL_LIB)/$(SO_TARGET): $(OBJ)
	@mkdir -p $(INSTALL_LIB)
	@mkdir -p $(INSTALL_INCLUDE)
	@mkdir -p $(INSTALL_DOC)
	$(CC) $(SO_OPTS) $^ -o $@ $(LDLIBS)
	( cd $(INSTALL_LIB) ; ln -sf $(SO_TARGET) $(SO_PLAIN) )
	( cd $(INSTALL_LIB) ; ln -sf $(SO_TARGET) $(SO_MAIN) )
	$(CP) ../Include/colamd.h $(INSTALL_INCLUDE)
	$(CP) ../README.txt $(INSTALL_DOC)/COLAMD_README.txt
	chmod 755 $(INSTALL_LIB)/$(SO_TARGET)
	chmod 644 $(INSTALL_INCLUDE)/colamd.h
	chmod 644 $(INSTALL_DOC)/COLAMD_README.txt

uninstall:
	$(RM) $(INSTALL_LIB)/$(SO_TARGET)
	$(RM) $(INSTALL_LIB)/$(SO_PLAIN)
	$(RM) $(INSTALL_LIB)/$(SO_MAIN)
	$(RM) $(INSTALL_INCLUDE)/colamd.h
	$(RM) $(INSTALL_DOC)/COLAMD_README.txt

