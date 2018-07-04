
twopi_files = $(wildcard *.twopi)
dot_files   = $(wildcard *.dot)
png_files  += $(patsubst %.dot,%.png,$(dot_files))
png_files  += $(patsubst %.twopi,%.png,$(twopi_files))
c_files     = $(wildcard *.c)

default: icl.pdf

icl.pdf: build_2.log
	@pdflatex                  \
	    -file-line-error       \
		-shell-escape          \
		-halt-on-error         \
		icl.tex                \
		> build_pdf.log        \
		2> err_pdf.pdf.log

build_2.log: build_1.log
	@pdflatex                  \
		-draftfile             \
	    -file-line-error       \
		-shell-escape          \
		-halt-on-error         \
		icl.tex                \
		> build_2.log          \
		2> err_2.log

build_1.log: icl.tex $(png_files) $(c_files)
	@pdflatex                  \
	    -file-line-error       \
		-shell-escape          \
		-halt-on-error         \
		icl.tex                \
		> build_1.log          \
		2> err_1.log

%.png:: %.twopi
	twopi -Tpng $< -o $@

%.png:: %.dot
	dot -Tpng $< -o $@

clean:
	git clean -Xdf
