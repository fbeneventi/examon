include ../../config.mk

ifneq ($(UNAME),SunOS)
	LIB_LDFLAGS:=$(LDFLAGS) -Wl,-soname,libmosquittopp.so.${SOVERSION}
endif

.PHONY : clean install

all : libmosquittopp.so.${SOVERSION} libmosquitto.a

install : all
	$(INSTALL) -d ${DESTDIR}$(prefix)/lib${LIB_SUFFIX}/
	$(INSTALL) -s --strip-program=$(STRIP) libmosquittopp.so.${SOVERSION} ${DESTDIR}${prefix}/lib${LIB_SUFFIX}/libmosquittopp.so.${SOVERSION}
	ln -sf libmosquittopp.so.${SOVERSION} ${DESTDIR}${prefix}/lib${LIB_SUFFIX}/libmosquittopp.so
	$(INSTALL) -d ${DESTDIR}${prefix}/include/
	$(INSTALL) mosquittopp.h ${DESTDIR}${prefix}/include/mosquittopp.h
	
uninstall :
	-rm -f ${DESTDIR}${prefix}/lib${LIB_SUFFIX}/libmosquittopp.so.${SOVERSION}
	-rm -f ${DESTDIR}${prefix}/lib${LIB_SUFFIX}/libmosquittopp.so
	-rm -f ${DESTDIR}${prefix}/include/mosquittopp.h

clean :
	-rm -f *.o libmosquittopp.so.${SOVERSION} libmosquittopp.a

libmosquittopp.so.${SOVERSION} : mosquittopp.o
	$(CXX) -shared $(LIB_LDFLAGS) $< -o $@ ../libmosquitto.so.${SOVERSION}

mosquittopp.o : mosquittopp.cpp mosquittopp.h
	$(CXX) $(LIB_CXXFLAGS) -c $< -o $@

libmosquitto.a : mosquittopp.o
	ar ru libmosquittopp.a mosquittopp.o
	ranlib libmosquittopp.a
