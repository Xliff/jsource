READLINE=1
ifeq (1,${DEBUG})
FDEBUG = /FS /Zi /DDEBUG=1
LDEBUG = /DEBUG
endif

ifeq (1,${x64})
CFLAGS= ${FDEBUG} /WX /W3 /Ot /Ob1 /GS /D_USING_V110_SDK71_ /D_CRT_SECURE_NO_WARNINGS /MT
FLAGS= ${LDEBUG} /STACK:0x10000000 /MACHINE:X64 /SUBSYSTEM:CONSOLE,5.02
else
CFLAGS= ${FDEBUG} /WX /W3 /Ot /Ob1 /Oy- /GS /D_USING_V110_SDK71_ /D_CRT_SECURE_NO_WARNINGS /MT
FLAGS= ${LDEBUG} /STACK:0x10000000 /MACHINE:X86 /SUBSYSTEM:CONSOLE,5.01
endif

.SUFFIXES: .o

OBJS=  \
 ../../jsrc/jconsole.o \
 ../../jsrc/jeload.o

ifdef READLINE
OBJSLN=  ../../jsrc/linenoise.o
CFLAGSLN= -DREADLINE -DUSE_LINENOISE
endif

RCS= ../../makevs/jconsole/jconsole.rc

ifndef LD
LD=link
endif

%.o: %.c
	$(CC) $(CFLAGS) $(CFLAGSLN) /Fo$@ /c $<

ifeq (1,${x64})
TARGET= jconsole.exe
else
TARGET= jconsole32.exe
endif

$(TARGET) : $(OBJS) $(OBJSLN) jconsole.res
	$(LD) /NOLOGO $(FLAGS) /out:$@ $(OBJS) $(OBJSLN) jconsole.res

jconsole.res : $(RCS)
	$(RC) /L 0x409 /D_USING_V110_SDK71_ -R -FO$@ $(RCS)

all: $(TARGET)

clean:
	rm -f *.res *.ilk *.pdb $(OBJS) $(OBJSLN)

.PHONY: all clean
