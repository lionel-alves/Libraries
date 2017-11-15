CC=clang
LD=clang
LIB_TOOL=clang
EXECUTABLE=bar
LDFLAGS=-framework CoreFoundation -lSystem

all: bar bar_static info

bar: main.o libmanhattan
	$(LD) $< -L. -lmanhattan -o $@

bar_static: main.o libmanhattan_static
	$(LD)  $< -L. -lmanhattan_static -o $@ $(LDFLAGS)

libmanhattan: manhattan.o
	$(CC) -dynamiclib manhattan.o -o libmanhattan.dylib $(LDFLAGS) 

libmanhattan_static: manhattan.o
	ar cru libmanhattan_static.a manhattan.o

.c.o:
	$(CC) -c $< -o %@

info:
	nm $(EXECUTABLE)
	otool -L $(EXECUTABLE)
	nm $(EXECUTABLE)_static
	otool -L $(EXECUTABLE)_static

clean:
	rm *.o *.dylib *.a bar
