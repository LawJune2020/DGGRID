TARGET = appex
SRCS = $(wildcard *.cpp)
OBJS = $(SRCS:.cpp=.o)
DEPS = $(SRCS:.cpp=.depends)
include ../../MakeIncludes
DGLIBDIR = ../../lib/dglib
SHPLIBDIR = ../../lib/shapelib
PROJ4LIBDIR = ../../lib/proj4lib
INCDIRS = -I$(DGLIBDIR)/include -I$(SHPLIBDIR)/include \
   -I$(PROJ4LIBDIR)/include $(ADD_INC_DIRS)
CCFLAGS  = ${INCDIRS} ${ADD_CPP_FLAGS} 
LDLIBS= $(DGLIBDIR)/lib/dglib.a \
        $(SHPLIBDIR)/lib/shapelib.a \
        $(PROJ4LIBDIR)/lib/proj4lib.a ${ADD_LD_LIBS}

.PHONY: clean all

all: $(TARGET)

${TARGET}: $(SRC) $(OBJS) $(DEPS) $(LDLIBS)
	${CPPCOMP} $(CCFLAGS) $(EXPORT) -o ${TARGET} ${OBJS} $(LDLIBS)

%.o: %.cpp
	$(CPPCOMP) -c $< $(CCFLAGS) -o $@

link:
	${CPPCOMP} $(CCFLAGS) $(EXPORT) -o ${TARGET} ${OBJS} $(LDLIBS)

%.depends: %.cpp
	$(CPPCOMP) -M $(CCFLAGS) $< > $@

$(LDLIBS):
	cd $(SHPLIBDIR)/lib; ${MAKE}
	cd $(PROJ4LIBDIR)/lib; ${MAKE}
	cd $(DGLIBDIR)/lib; ${MAKE}

clean:
	rm -rf $(OBJS) $(DEPS) ${TARGET} core ti_files ii_files

-include $(DEPS)

