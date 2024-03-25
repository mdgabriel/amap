PDFLATEX      := TEXINPUTS=.:$(PWD):: lualatex
PDFREADER     := evince
PANDOC        := pandoc -f latex -t odt
DERIVED_FILES := *.aux *.bbl *.blg *.dvi *.idx *.ilg \
		 *.lof *.log *.lot *.out *.toc *.4ct \
		 *.4tc *.4og *.css *.idv *.xref *.lg \
		 *.tmp
JPG_FILES     := $(wildcard *.jpg)
CLS_FILES     := $(wildcard *.cls)
STY_FILES     := $(wildcard *.sty)
IMG_FILES     := $(wildcard *.png) $(wildcard *.jpg) $(wildcard *.jpeg)
TEX_FILES     := $(wildcard *.tex)
ODT_FILES     := $(patsubst %.tex,%.pandoc.odt,$(TEX_FILES))
PDF_FILES     := $(patsubst %.tex,%.pdf,$(TEX_FILES))

.PHONY: all read clean realclean install

all: $(PDF_FILES) $(ODT_FILES)

read: $(PDF_FILES)
	$(PDFREADER) $(PDF_FILES)

%.pdf: %.tex $(JPG_FILES) $(CLS_FILES) $(STY_FILES) Makefile
	$(PDFLATEX) $(<F)
	$(PDFLATEX) $(<F)

%.pandoc.odt: %.tex $(CLS_FILES) $(STY_FILES) Makefile
	$(PANDOC) -o $(patsubst %.tex,%.pandoc.odt,$(<F)) $(<F)

clean:
	rm -f $(DERIVED_FILES)

realclean: clean
	rm -f $(PDF_FILES) $(ODT_FILES)

install: $(PDF_FILES) $(ODT_FILES)
	cp $? ${HOME}/Downloads/.
