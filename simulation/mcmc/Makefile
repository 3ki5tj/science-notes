prj=mcmc

figs=
pdffigs=$(patsubst %,fig/%.pdf, $(figs))
epsfigs=$(patsubst %,fig/%.eps, $(figs))
figgps=$(patsubst %,fig/%.gp,  $(figs))

texs = $(wildcard *.tex)
pdfs = $(patsubst %.tex,%.pdf, $(texs))

all: $(pdfs)

$(pdfs): %.pdf: %.tex Makefile $(pdffigs)
	#pdflatex $<
	#bibtex $*
	pdflatex $<
	pdflatex $<

$(pdffigs): %.pdf: %.gp
	$(MAKE) -C fig

clean:
	$(RM) *.aux *.bbl *.blg *.log *.dvi *.out \
	      *Notes.bib *~
	rstrip.py

$(prj)doc.zip: $(prj).tex $(prj).pdf \
	       $(epsfigs) $(pdffigs) $(figgps) \
	       README Makefile
	zip -r $@ $^

zip: $(prj)doc.zip

Bossman:
	rsync -avL $(pdfs) $(texs) \
	  /Bossman/cz1/notes/$(prj)
	rsync -avL prog/*.c prog/*.html \
	  /Bossman/cz1/notes/$(prj)/prog/

#cz1@129.109.88.204:/Bossman/cz1/notes/$(prj)
