OBO=http://purl.obolibrary.org/obo
SRC = ../cl-basic.obo
TGTS = html text rss
ONT= cl
OWLSRC = ../$(ONT).owl
LAST = $(OBO)/$(ONT).obo
OWLLAST = $(OBO)/$(ONT).owl

TXTS = $(ONT)-obo-diff.txt $(ONT)-def-diff.txt

###removing owljs dependency for now
###all: $(ONT)-obo-diff.html $(ONT)-def-diff.html $(ONT)-combined-diff.txt $(ONT)-diff.md
all: 
###all: $(ONT)-obo-diff.html $(ONT)-def-diff.html $(ONT)-combined-diff.txt

$(ONT)-obo-diff.html: $(ONT)-lastbuild.obo $(SRC)
	compare-obo-files.pl --config 'html/ontology_name=Cell Ontology' --rss-path . -f1 $< -f2 $(SRC) -m $(TGTS) -o $(ONT)-obo-diff
$(ONT)-def-diff.html: $(ONT)-lastbuild.obo $(SRC)
	compare-defs.pl --config 'html/ontology_name=Cell Ontology' --rss-path . -f1 $< -f2 $(SRC) -m $(TGTS) -o $(ONT)-def-diff

$(ONT)-obo-diff.txt: $(ONT)-obo-diff.html
$(ONT)-def-diff.txt: $(ONT)-def-diff.html

$(ONT)-combined-diff.txt:  $(TXTS)
	cat $(TXTS) > $@

$(ONT)-lastbuild.obo: $(SRC)
	wget --no-check-certificate $(OBO)/$(ONT)-basic.obo -O $@
$(ONT)-lastbuild.owl: $(SRC)
	wget --no-check-certificate $(OWLLAST) -O $@ && touch $@

$(ONT)-diff.md: $(ONT)-lastbuild.owl $(OWLSRC)
	owljs-diff -C ../catalog-v001.xml -o $@ $< $(OWLSRC) 
