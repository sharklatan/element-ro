

HAVE_MYSQL=yes
ifeq ($(HAVE_MYSQL),yes)
	ALL_DEPENDS=common common_sql login login_sql char char_sql map map_sql ladmin tools converters plugins import save
	SQL_DEPENDS=common_sql login_sql char_sql map_sql import save
	COMMON_SQL_DEPENDS=
	LOGIN_SQL_DEPENDS=common_sql
	CHAR_SQL_DEPENDS=common_sql
	MAP_SQL_DEPENDS=common_sql
	CONVERTERS_DEPENDS=common_sql
else
	ALL_DEPENDS=common login char map ladmin tools plugins import save
	SQL_DEPENDS=needs_mysql
	COMMON_SQL_DEPENDS=needs_mysql
	LOGIN_SQL_DEPENDS=needs_mysql
	CHAR_SQL_DEPENDS=needs_mysql
	MAP_SQL_DEPENDS=needs_mysql
	CONVERTERS_DEPENDS=needs_mysql
endif

#####################################################################
.PHONY: txt sql conf \
	common common_sql \
	login login_sql \
	char char_sql \
	map map_sql \
	ladmin tools converters plugins addons import save \
	clean help

all: $(ALL_DEPENDS)

txt: common login char map import save

sql: $(SQL_DEPENDS)

conf: import save

common:
	@$(MAKE) -C src/common txt

common_sql: $(COMMON_SQL_DEPENDS)
	@$(MAKE) -C src/common sql

login: common
	@$(MAKE) -C src/login

login_sql: $(LOGIN_SQL_DEPENDS)
	@$(MAKE) -C src/login_sql

char: common
	@$(MAKE) -C src/char

char_sql: $(CHAR_SQL_DEPENDS)
	@$(MAKE) -C src/char_sql

map: common
	@$(MAKE) -C src/map txt

map_sql: $(MAP_SQL_DEPENDS)
	@$(MAKE) -C src/map sql

ladmin: common
	@$(MAKE) -C src/ladmin

tools:
	@$(MAKE) -C src/tool

converters: $(CONVERTERS_DEPENDS)
	@$(MAKE) -C src/txt-converter

plugins addons: common
	@$(MAKE) -C src/plugins

import:
# 1) create conf/import folder
# 2) add missing files
# 3) remove remaining .svn folder
	@echo "building conf/import folder..."
	@if test ! -d conf/import ; then mkdir conf/import ; fi
	@for f in $$(ls conf/import-tmpl) ; do if test ! -e conf/import/$$f ; then cp conf/import-tmpl/$$f conf/import ; fi ; done
	@rm -rf conf/import/.svn

save:
# 1) create save folder
# 2) add missing files
# 3) remove remaining .svn folder
	@echo "building save folder..."
	@if test ! -d save ; then mkdir save ; fi
	@for f in $$(ls save-tmpl) ; do if test ! -e save/$$f ; then cp save-tmpl/$$f save ; fi ; done
	@rm -rf save/.svn

clean:
	@$(MAKE) -C src/common $@
	@$(MAKE) -C src/login $@
	@$(MAKE) -C src/login_sql $@
	@$(MAKE) -C src/char $@
	@$(MAKE) -C src/char_sql $@
	@$(MAKE) -C src/map $@
	@$(MAKE) -C src/ladmin $@
	@$(MAKE) -C src/plugins $@
	@$(MAKE) -C src/tool $@
	@$(MAKE) -C src/txt-converter $@

help:
	@echo "most common targets are 'all' 'txt' 'sql' 'conf' 'clean' 'help'"
	@echo "possible targets are:"
	@echo "'common'      - builds object files used in TXT servers"
	@echo "'common_sql'  - builds object files used in SQL servers"
	@echo "'login'       - builds login server (TXT version)"
	@echo "'login_sql'   - builds login server (SQL version)"
	@echo "'char'        - builds char server (TXT version)"
	@echo "'char_sql'    - builds char server (SQL version)"
	@echo "'map'         - builds map server (TXT version)"
	@echo "'map_sql'     - builds map server (SQL version)"
	@echo "'ladmin'      - builds remote administration tool"
	@echo "'tools'       - builds all the tools in src/tools"
	@echo "'converters'  - builds the login/char converters"
	@echo "'plugins'     - builds all the plugins in src/plugins"
	@echo "'addons'"
	@echo "'import'      - builds conf/import folder from the template conf/import-tmpl"
	@echo "'save'        - builds save folder from the template save-tmpl"
	@echo "'all'         - builds all the above targets"
	@echo "'txt'         - builds txt servers (targets 'common' 'login' 'char' 'map'"
	@echo "                'import' and 'save')"
	@echo "'sql'         - builds sql servers (targets 'common_sql' 'login_sql' 'char_sql'"
	@echo "                'map_sql' 'import' and 'save')"
	@echo "'conf'        - builds templated folders/files (targets 'import' and 'save')"
	@echo "'clean'       - cleans builds and objects"
	@echo "'help'        - outputs this message"

#####################################################################

needs_mysql:
	@echo "MySQL not found or disabled by the configure script"
	@exit 1

#####################################################################
# TODO

install:	conf/%.conf conf/%.txt
	$(shell read -p "WARNING: This target does not work properly yet. Press Ctrl+C to cancel or Enter to continue.")
	$(shell mkdir -p /opt/eathena/bin/)
	$(shell mkdir -p /opt/eathena/etc/eathena/)
	$(shell mkdir -p /opt/eathena/var/log/eathena/)
	$(shell mv save /opt/eathena/etc/eathena/save)
	$(shell mv db /opt/eathena/etc/eathena/db)
	$(shell mv conf /opt/eathena/etc/eathena/conf)
	$(shell mv npc /opt/eathena/etc/eathena/npc)
	$(shell mv log/* /opt/eathena/var/log/eathena/)
	$(shell cp *-server* /opt/eathena/bin/)
	$(shell cp ladmin /opt/eathena/bin/)
	$(shell ln -s /opt/eathena/etc/eathena/save/ /opt/eathena/bin/)
	$(shell ln -s /opt/eathena/etc/eathena/db/ /opt/eathena/bin/)
	$(shell ln -s /opt/eathena/etc/eathena/conf/ /opt/eathena/bin/)
	$(shell ln -s /opt/eathena/etc/eathena/npc/ /opt/eathena/bin/)
	$(shell ln -s /opt/eathena/var/log/eathena/ /opt/eathena/bin/log)

bin-clean:
	$(shell rm /opt/eathena/bin/login-server*)
	$(shell rm /opt/eathena/bin/char-server*)
	$(shell rm /opt/eathena/bin/map-server*)
	$(shell rm /opt/eathena/bin/ladmin)

uninstall:
	$(shell read -p "WARNING: This target does not work properly yet. Press Ctrl+C to cancel or Enter to continue.")
	bin-clean
	$(shell rm /opt/eathena/bin/save)
	$(shell rm /opt/eathena/bin/db)
	$(shell rm /opt/eathena/bin/conf)
	$(shell rm /opt/eathena/bin/npc)
	$(shell rm /opt/eathena/bin/log)
	$(shell rm -rf /opt/eathena/etc/eathena)
	$(shell rm -rf /opt/eathena/var/log/eathena)
