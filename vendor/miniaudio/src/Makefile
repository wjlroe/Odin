OS:=$(shell uname)

ifeq ($(OS), Darwin)
all: darwin
else
all: unix
endif

unix:
	mkdir -p ../lib
	$(CC) -c -O2 -Os -fPIC miniaudio.c
	$(AR) rcs ../lib/miniaudio.a miniaudio.o
	#$(CC) -fPIC -shared -Wl,-soname=miniaudio.so -o ../lib/miniaudio.so miniaudio.o
	rm *.o

darwin:
	mkdir -p ../lib/darwin
	$(CC) -c -O2 -Os -fPIC -arch x86_64 -mmacosx-version-min=10.12 miniaudio.c -o miniaudio-x86_64.o
	$(CC) -c -O2 -Os -fPIC -arch arm64 -mmacosx-version-min=10.12 miniaudio.c -o miniaudio-arm64.o
	lipo -create miniaudio-x86_64.o miniaudio-arm64.o -output ../lib/darwin/miniaudio.a
	rm *.o
