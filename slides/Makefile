#DEFINITIONS

slides_sections := $(shell grep 'input{' slides.tex | grep -v '%.*input' | sed 's/^.*input{\(.*\.tex\).*/\1/')
tex_inputs := $(shell grep --no-filename -o 'input{[A-Za-z0-9_\/\.]*}' $(slides_sections) | sed 's/input{//' | sed 's/\.tex}/.tex/')
img_inputs := $(shell grep 'includegraphics' $(slides_sections) | grep -v '%.*includegraphics' | sed 's/^.*includegraphics\[.*\]{\([\./a-zA-Z0-9_]*\)}.*/\1/')
csv_inputs := $(shell grep 'input{.*\.csv}' $(slides_sections) | grep -v '%.*input' | sed 's/^.*input{\(.*\.csv\).*/\1/')

#RECIPES

all: slides.pdf

clean:
	rm *.log *.aux
	rm *.out

input/:
	mkdir $@

slides.pdf: slides.tex $(slides_sections) $(tex_inputs) $(img_inputs) $(csv_inputs)
	#module load texlive
	pdflatex -draftmode $<
	pdflatex -draftmode $<
	pdflatex $<
	rm slides.log slides.aux slides.out slides.toc
	rm slides.snm slides.nav
	rm slides.blg slides.bbl	
	#module unload texlive
#INPUTS
DiD_Results = $(foreach did_hist did_plot did_treatmenteffect_plot votershare_histogram, ../input/$(did_hist).png)
input/did_hist.png input/did_plot.png input/did_treatmenteffect_plot.png input/votershare_histogram.png : input/%: ../tasks/DiD_offmenuspending_results/output/%
	cp $< $@
$(addprefix input/, Full_IK_MSE_CER_Bandwidth_comparison_table.tex Full_IK_MSE_CER_Bandwidth_comparison_table_beauty.tex placebo_test_effects.png placebo_test_pvalue.png rdd_density.png RDD_plot.png RDD_statistics.tex off_menu_expenditures_histogram.png voteshare_histogram.png): input/%: ../tasks/estimate_RDD_model/output/%
	cp $< $@