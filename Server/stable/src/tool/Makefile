


#####################################################################
.PHONY : all adduser convert mapcache clean help

all: adduser convert mapcache

adduser:
	gcc -o ../../tools/adduser.exe adduser.c

convert:
	gcc -o ../../tools/convert.exe convert.c

mapcache: obj_mapcache
	gcc -c -o obj_mapcache/grfio.o grfio.c
	gcc -o ../../mapcache.exe mapcache.c obj_mapcache/grfio.o -lz

clean:
	rm -rf *.o obj_mapcache ../../tools/adduser.exe ../../tools/convert.exe ../../mapcache.exe

help:
	@echo "possible targets are 'adduser' 'convert' 'mapcache' 'all' 'clean' 'help'"
	@echo "'adduser'   - ???"
	@echo "'convert'   - ???"
	@echo "'mapcache'  - mapcache generator"
	@echo "'all'       - builds all above targets"
	@echo "'clean'     - cleans builds and objects"
	@echo "'help'      - outputs this message"

#####################################################################

obj_mapcache:
	-mkdir obj_mapcache
