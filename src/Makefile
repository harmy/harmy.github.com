PELICAN=pelican
PELICANOPTS=-v

BASEDIR=$(PWD)
OUTPUTDIR=$(BASEDIR)/..
CONFFILE=$(BASEDIR)/settings.py

help:
	@echo 'Makefile for a pelican Web site                                        '
	@echo '                                                                       '
	@echo 'Usage:                                                                 '
	@echo '   make html                        (re)generate the web site          '
	@echo '   make clean                       remove the generated files         '
	@echo '   make regenerate                  regenerate files upon modification '
	@echo '   make serve                       serve site at http://localhost:8000'
	@echo '   make devserver                   start/restart develop_server.sh    '
	@echo '                                                                       '


html: clean $(OUTPUTDIR)/index.html
	@echo 'Done'

$(OUTPUTDIR)/%.html:
	$(PELICAN) -o $(OUTPUTDIR) -s $(CONFFILE) $(PELICANOPTS)

clean:
	cd ..;rm -rf `ls |egrep -v "CNAME|src"`

regenerate: clean
	$(PELICAN) -r -o $(OUTPUTDIR) -s $(CONFFILE) $(PELICANOPTS)

serve:
	cd $(OUTPUTDIR) && python -m SimpleHTTPServer

devserver:
	$(BASEDIR)/develop_server.sh restart


.PHONY: html help clean regenerate serve devserver
