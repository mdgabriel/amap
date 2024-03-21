PDFLATEX      := TEXINPUTS=.:$(PWD):: lualatex
PDFREADER     := evince
PANDOC        := pandoc -f latex -t odt
DERIVED_FILES := *.aux *.bbl *.blg *.dvi *.idx *.ilg \
		 *.lof *.log *.lot *.out *.toc *.4ct \
		 *.4tc *.4og *.css *.idv *.xref *.lg \
		 *.tmp *.pandoc.odt
CLS_FILES     := $(wildcard *.cls)
STY_FILES     := $(wildcard *.sty)
IMG_FILES     := $(wildcard *.png) $(wildcard *.jpg) $(wildcard *.jpeg)
TEX_FILES     := $(wildcard *.tex)
ODT_FILES     := $(patsubst %.tex,%.odt,$(TEX_FILES))
PDF_FILES     := $(patsubst %.tex,%.pdf,$(TEX_FILES))

.PHONY: all read clean realclean

all: $(PDF_FILES) $(ODT_FILES)

read: $(PDF_FILES)
	$(PDFREADER) $(PDF_FILES)

%.pdf: %.tex $(CLS_FILES) $(STY_FILES) Makefile
	$(PDFLATEX) $(<F)
	$(PDFLATEX) $(<F)

%.odt: %.tex $(CLS_FILES) $(STY_FILES) Makefile
	$(PANDOC) -o $(patsubst %.tex,%.pandoc.odt,$(<F)) $(<F)

clean:
	rm -f $(DERIVED_FILES)

realclean: clean
	rm -f $(PDF_FILES)
