
COMMON_OBJ = ../common/obj_all/core.o ../common/obj_all/socket.o ../common/obj_all/timer.o \
	../common/obj_all/db.o ../common/obj_all/plugins.o ../common/obj_all/lock.o \
	../common/obj_all/malloc.o ../common/obj_all/showmsg.o ../common/obj_all/utils.o \
	../common/obj_all/strlib.o ../common/obj_all/grfio.o \
	../common/obj_all/mapindex.o ../common/obj_all/ers.o
COMMON_H = ../common/core.h ../common/socket.h ../common/timer.h ../common/mmo.h \
	../common/version.h ../common/db.h ../common/plugins.h ../common/lock.h \
	../common/malloc.h ../common/showmsg.h ../common/utils.h \
	../common/strlib.h ../common/grfio.h \
	../common/mapindex.h ../common/ers.h

CHAR_OBJ = obj_txt/char.o obj_txt/inter.o obj_txt/int_party.o obj_txt/int_guild.o \
	obj_txt/int_storage.o obj_txt/int_status.o obj_txt/int_pet.o obj_txt/int_homun.o
CHAR_H = char.h inter.h int_party.h int_guild.h int_storage.h int_status.h int_pet.h int_homun.h



#####################################################################
.PHONY : all char-server clean help

all: char-server

char-server: obj_txt $(CHAR_OBJ) $(COMMON_OBJ)
	gcc  -L/usr/lib -o ../../char-server.exe $(CHAR_OBJ) $(COMMON_OBJ) -lm -lz 

clean:
	rm -rf *.o obj_txt ../../char-server.exe

help:
	@echo "possible targets are 'char-server' 'all' 'clean' 'help'"
	@echo "'char-server'  - char server (TXT version)"
	@echo "'all'          - builds all above targets"
	@echo "'clean'        - cleans builds and objects"
	@echo "'help'         - outputs this message"

#####################################################################

obj_txt:
	-mkdir obj_txt

obj_txt/%.o: %.c $(CHAR_H) $(COMMON_H)
	gcc -g -O2 -pipe -ffast-math -Wall -Wno-sign-compare -Wno-unused-parameter -Wno-switch -DTXT_ONLY  -I../common -I/usr/include -DFD_SETSIZE=4096 -DCYGWIN -c $(OUTPUT_OPTION) $<

# missing common object files
../common/obj_all/%.o:
	@$(MAKE) -C ../common txt
