# Change history:
SHELL=bash
OS:=$(shell uname)
CC="g++${GCCVER}" # Mind specifics for Darwin 10.x
LD="gcc${GCCVER}" # Mind specifics for Darwin 10.x
ARCH=64

TOP=../..
WD=../..
$(Invoking: GCC C Linker)
all: XFMC
	@echo "Compile done"
c_SRC+=${WD}/source/fmc.c 
c_SRC+=${WD}/source/graphics.c
c_SRC+=${WD}/source/route.c
c_SRC+=${WD}/source/legspage.c
c_SRC+=${WD}/source/vnav.c
c_SRC+=${WD}/source/calculations.c
c_SRC+=${WD}/source/airplaneparameters.c
c_SRC+=${WD}/source/hold.c
c_SRC+=${WD}/source/menu.c
c_SRC+=${WD}/source/performance.c
c_SRC+=${WD}/source/plugins.c
c_SRC+=${WD}/source/progress.c
c_SRC+=${WD}/source/radios.c
c_SRC+=${WD}/source/sound.c
c_SRC+=${WD}/source/thrustlimit.c
c_SRC+=${WD}/source/stb_image_aug.c
c_SRC+=${WD}/source/runways.c
c_SRC+=${WD}/source/hsi.c
c_SRC+=${WD}/source/terminalproc.c

	
OBJS+=$(c_SRC:.c=.o)

OBJS+=$(cpp_SRC:.cpp=.cpp.o)

CFLAGS+=  -I${WD}/libraries/XP_SDK/CHeaders/XPLM 
CFLAGS+=  -I${WD}/libraries/freetype-2.5.2/include

CFLAGS+= 

DBG=-g
CFLAGS+=-fpermissive -fno-stack-protector -Wall -w -x c++ -ansi



# Handle Linux/OS X specific stuff here.

ifeq	(${OS},Linux) 
	
	ifeq (${ARCH}, 32)
	LIBVER=
	endif
	ifeq (${ARCH}, 64)
	LIBVER=64
	endif
	LIBS+=-Wl,-rpath,'$$ORIGIN'
	LIBS+=-L${WD}/libraries/FMOD/Linux/api/lib/libfmodex${LIBVER}.so
	LIBS+=-L${WD}/libraries/freetype-2.5.2/libs/Linux/libfreetype${LIBVER}.a
	LIBS+=-Wl,--version-script=${WD}/build/unix/linker.script
	
	CFLAGS+=  -I${WD}/libraries/FMOD/Linux/api/inc
	CFLAGS+=-m${ARCH} -DXPLM200=1 -DXPLM210=1 -DLIN=1 -fPIC -O3 -Wall -fno-strict-aliasing -lGL -lGLU

	LDFLAGS+=-m${ARCH} -shared -rdynamic -nodefaultlibs -undefined_warning -fvisibility=hidden 

endif
ifeq (${OS}, Darwin)
        OS_VER=$(shell uname -r | sed 's/\([0-9]*\).*/\1/')
        ifeq (${OS_VER}, 10)
            CC=g++-4.0
            LD=gcc-4.0
        endif
	
	ifeq (${ARCH}, 32)
	FMODEX=fmodex
	LIBFREETYPE=freetype32
	endif
	ifeq (${ARCH}, 64)
	FMODEX=fmodex
	LIBFREETYPE=freetype64
	endif
	CFLAGS+=  -I${WD}/FMOD/Mac/api/inc
	LIBS+= -L${WD}/FMOD/Mac/api/lib -l${FMODEX} 
	LIBS+= -L${WD}/Freetypelib/MacOS -l${LIBFREETYPE} 
	CFLAGS+= -m${ARCH} -DAPPLE -DAPL=1  -DLIN=0 -DIBM=0 -O3 -fpascal-strings \
	 -I../MacIncludes \
	  -funsigned-char \
	  -arch i386 -mmacosx-version-min=10.4 \
	  -iquote../FMOD/FMODMac/api/inc \
	  -isysroot /Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.8.sdk 
	LDFLAGS+=-m${ARCH} -flat_namespace -undefined suppress
	LDFLAGS+= -bundle -framework Carbon -framework OpenGL -framework ApplicationServices
	LDFLAGS+= -arch i386 -mmacosx-version-min=10.4
	LDFLAGS+= -Wl,-syslibroot,/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.8.sdk
	FINAL=
	
endif
clean:  
	@echo ¨cleaning objs¨
	rm -f ${OBJS}
	rm -f XFMC32.xpl
	rm -f XFMC64.xpl

XFMC:	${OBJS} 
	${LD} ${LDFLAGS} -o ./XFMC${ARCH}.xpl ${OBJS}$ ${LIBS} 

Xfmc_32.xpl: fmc.c
	${CC} -c  ${CFLAGS} ${c_SRC} 


