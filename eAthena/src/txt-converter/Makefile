
LOGIN_CONVERTER_OBJ = obj_login/login-converter.o ../common/obj_all/minicore.o \
	../common/obj_all/malloc.o ../common/obj_all/strlib.o ../common/obj_all/showmsg.o \
	../common/obj_all/utils.o ../common/obj_all/ers.o ../common/obj_all/db.o \
	../common/obj_sql/sql.o
LOGIN_CONVERTER_H = ../common/cbasetypes.h ../common/mmo.h ../common/core.h \
	../common/malloc.h ../common/strlib.h ../common/showmsg.h \
	../common/utils.h ../common/ers.h ../common/db.h \
	../common/sql.h

CHAR_CONVERTER_OBJ = obj_char/char-converter.o \
	obj_char/txt-char.o obj_char/txt-int_pet.o obj_char/txt-int_storage.o obj_char/txt-inter.o \
	obj_char/txt-int_party.o obj_char/txt-int_guild.o \
	obj_char/sql-char.o obj_char/sql-int_pet.o obj_char/sql-int_storage.o \
	obj_char/sql-inter.o obj_char/sql-int_party.o obj_char/sql-int_guild.o \
	../common/obj_all/minicore.o \
	../common/obj_all/malloc.o ../common/obj_all/strlib.o ../common/obj_all/showmsg.o \
	../common/obj_all/utils.o ../common/obj_all/ers.o ../common/obj_all/mapindex.o \
	../common/obj_sql/sql.o
CHAR_CONVERTER_H = ../char/char.h ../char/int_pet.h ../char/int_storage.h ../char/inter.h \
	../char/int_party.h ../char/int_guild.h \
	../char_sql/char.h ../char_sql/int_pet.h ../char_sql/int_storage.h \
	../char_sql/inter.h ../char_sql/int_party.h ../char_sql/int_guild.h \
	../common/cbasetypes.h ../common/mmo.h ../common/core.h \
	../common/malloc.h ../common/strlib.h ../common/showmsg.h \
	../common/utils.h ../common/ers.h ../common/mapindex.h \
	../common/sql.h

HAVE_MYSQL=yes
ifeq ($(HAVE_MYSQL),yes)
	LOGIN_CONVERTER_DEPENDS=obj_login $(LOGIN_CONVERTER_OBJ)
	CHAR_CONVERTER_DEPENDS=obj_char $(CHAR_CONVERTER_OBJ)
else
	LOGIN_CONVERTER_DEPENDS=needs_mysql
	CHAR_CONVERTER_DEPENDS=needs_mysql
endif



#####################################################################
.PHONY : all login-converter char-converter clean help

all: login-converter char-converter

login-converter: $(LOGIN_CONVERTER_DEPENDS)
	gcc  -L/usr/lib -o ../../tools/login-converter.exe $(LOGIN_CONVERTER_OBJ) -lm -lz  -L/usr/local/lib/mysql -lmysqlclient -lz -lcrypt -lm

char-converter: $(CHAR_CONVERTER_DEPENDS)
	gcc  -L/usr/lib -o ../../tools/char-converter.exe $(CHAR_CONVERTER_OBJ) -lm -lz  -L/usr/local/lib/mysql -lmysqlclient -lz -lcrypt -lm

clean:
	rm -rf *.o obj_login obj_char ../../tools/login-converter.exe ../../tools/char-converter.exe

help:
	@echo "possible targets are 'login-converter' 'char-converter' 'all' 'clean' 'help'"
	@echo "'login-converter'  - login server converter"
	@echo "'char-converter'   - char server converter"
	@echo "'all'              - builds all above targets"
	@echo "'clean'            - cleans builds and objects"
	@echo "'help'             - outputs this message"

#####################################################################

needs_mysql:
	@echo "MySQL not found or disabled by the configure script"
	@exit 1

obj_login:
	-mkdir obj_login

obj_char:
	-mkdir obj_char

obj_login/%.o: %.c $(LOGIN_CONVERTER_H)
	gcc -g -O2 -pipe -ffast-math -Wall -Wno-sign-compare -Wno-unused-parameter -Wno-switch -I/usr/local/include/mysql  -I../common -I/usr/include -DFD_SETSIZE=4096 -DCYGWIN -DTXT_SQL_CONVERT -c $(OUTPUT_OPTION) $<

obj_char/%.o: %.c $(CHAR_CONVERTER_H)
	gcc -g -O2 -pipe -ffast-math -Wall -Wno-sign-compare -Wno-unused-parameter -Wno-switch -I/usr/local/include/mysql  -I../common -I/usr/include -DFD_SETSIZE=4096 -DCYGWIN -DTXT_SQL_CONVERT -c $(OUTPUT_OPTION) $<

obj_char/txt-%.o: ../char/%.c $(CHAR_CONVERTER_H)
	gcc -g -O2 -pipe -ffast-math -Wall -Wno-sign-compare -Wno-unused-parameter -Wno-switch -I/usr/local/include/mysql  -I../common -I/usr/include -DFD_SETSIZE=4096 -DCYGWIN -DTXT_SQL_CONVERT -c $(OUTPUT_OPTION) $<

obj_char/sql-%.o: ../char_sql/%.c $(CHAR_CONVERTER_H)
	gcc -g -O2 -pipe -ffast-math -Wall -Wno-sign-compare -Wno-unused-parameter -Wno-switch -I/usr/local/include/mysql  -I../common -I/usr/include -DFD_SETSIZE=4096 -DCYGWIN -DTXT_SQL_CONVERT -c $(OUTPUT_OPTION) $<

# missing common object files
../common/obj_all/%.o:
	@$(MAKE) -C ../common sql

../common/obj_sql/%.o:
	@$(MAKE) -C ../common sql
