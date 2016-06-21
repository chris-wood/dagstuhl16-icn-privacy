PROJ      := crypto
OUT       := .
PDF       := $(OUT)/$(PROJ).pdf

CMDPDF    := pdflatex
PDFVIEWER := evince

all:
	$(CMDPDF) $(PROJ) $<
	bibtex $(PROJ)
	makeglossaries $(PROJ)
	$(CMDPDF) $(PROJ) $<
	$(CMDPDF) $(PROJ) $<

# Create the OUT directory, if it doesn't exist
$(OUT):
	mkdir -p $@

show	: $(PDF)
	$(PDFVIEWER) "$(PDF)"

clean	:
	rm -rf $(shell find $(OUT) -name '*~' -type f)
	rm -rf $(shell find $(OUT) -name '*.acn' -type f)
	rm -rf $(shell find $(OUT) -name '*.acr' -type f)
	rm -rf $(shell find $(OUT) -name '*.alg' -type f)
	rm -rf $(shell find $(OUT) -name '*.aux' -type f)
	rm -rf $(shell find $(OUT) -name '*.bbl' -type f)
	rm -rf $(shell find $(OUT) -name '*.blg' -type f)
	rm -rf $(shell find $(OUT) -name '*.dvi' -type f)
	rm -rf $(shell find $(OUT) -name '*.glg' -type f)
	rm -rf $(shell find $(OUT) -name '*.glo' -type f)
	rm -rf $(shell find $(OUT) -name '*.gls' -type f)
	rm -rf $(shell find $(OUT) -name '*.ist' -type f)
	rm -rf $(shell find $(OUT) -name '*.loa' -type f)
	rm -rf $(shell find $(OUT) -name '*.lof' -type f)
	rm -rf $(shell find $(OUT) -name '*.log' -type f)
	rm -rf $(shell find $(OUT) -name '*.lot' -type f)
	rm -rf $(shell find $(OUT) -name '*.out' -type f)
	rm -rf $(shell find $(OUT) -name '*.toc' -type f)
	rm -rf $(OUT)/*.pdf
