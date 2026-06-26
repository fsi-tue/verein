TEX = lualatex
TEXFLAGS = -interaction=nonstopmode -halt-on-error
SVGCONVERT = rsvg-convert
A5_TARGET = flyer-a5
A4_TARGET = flyer-a4
SOURCE = flyer.tex
LOGO_SVG = assets/vereins-denker.svg
LOGO_PDF = assets/vereins-denker.pdf
CACHE_DIR = .cache
TEXMFVAR_DIR = .texmf-var
BUILD_ENV = TEXMFVAR=$(CURDIR)/$(TEXMFVAR_DIR) XDG_CACHE_HOME=$(CURDIR)/$(CACHE_DIR)

.PHONY: all clean distclean

all: $(A5_TARGET).pdf $(A4_TARGET).pdf

$(A5_TARGET).pdf: $(SOURCE) $(LOGO_PDF) $(CACHE_DIR) $(TEXMFVAR_DIR)
	$(BUILD_ENV) $(TEX) $(TEXFLAGS) -jobname=$(A5_TARGET) $(SOURCE)
	$(BUILD_ENV) $(TEX) $(TEXFLAGS) -jobname=$(A5_TARGET) $(SOURCE)

$(A4_TARGET).pdf: $(A4_TARGET).tex $(A5_TARGET).pdf $(CACHE_DIR) $(TEXMFVAR_DIR)
	$(BUILD_ENV) $(TEX) $(TEXFLAGS) $(A4_TARGET).tex
	$(BUILD_ENV) $(TEX) $(TEXFLAGS) $(A4_TARGET).tex

$(LOGO_PDF): $(LOGO_SVG)
	$(SVGCONVERT) -f pdf -o $(LOGO_PDF) $(LOGO_SVG)

$(CACHE_DIR) $(TEXMFVAR_DIR):
	mkdir -p $@

clean:
	rm -f flyer.aux flyer.log flyer.out
	rm -f $(A5_TARGET).aux $(A5_TARGET).log $(A5_TARGET).out
	rm -f $(A4_TARGET).aux $(A4_TARGET).log $(A4_TARGET).out

distclean: clean
	rm -f flyer.pdf $(A5_TARGET).pdf $(A4_TARGET).pdf $(LOGO_PDF)
