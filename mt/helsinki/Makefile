

DATAHOME = ../data
SRC = en
TRG = fi

APPLHOME     = /homeappl/home/tiedeman/appl_taito
MOSESHOME    = ${APPLHOME}/tools/mosesdecoder
MOSESSCRIPTS = ${MOSESHOME}/scripts
TOKENIZER    = $(MOSESSCRIPTS)/tokenizer

SUBMISSIONS = 	run35.hyb2bpe.simple.1best.sgm \
		run35.hyb2bpe.simple.detok.sgm \
		test2017-run105abcd_run106abcd-ens-2-ens.txt.sgm \
		ep+rapid+news+back-news+cc-bpe.newstest2017-enfi.en.fi.sgm \
		nmt-preMT30-45k.sgm \
		run35.hyb2bpe.10best.1best.sgm \
		run35.hyb2bpe.nonorm.1best.sgm \
		run35.hyb2bpe.ens.1best.sgm


all: ${SUBMISSIONS}


%.detok: %
	$(TOKENIZER)/replace-unicode-punctuation.perl < $< |\
	$(TOKENIZER)/remove-non-printing-char.perl |\
	$(TOKENIZER)/normalize-punctuation.perl -l $(TRG) |\
	$(MOSESSCRIPTS)/tokenizer/detokenizer.perl -l ${TRG} |\
	sed 's/\([0-9]\) - \([0-9|a-z]\)/\1-\2/g' |\
	sed 's# / #/#g' > $@


%.sgm: %
	${MOSESSCRIPTS}/ems/support/wrap-xml.perl \
		${TRG} ${DATAHOME}/test/newstest2017-${SRC}${TRG}-src.${SRC}.sgm HY \
		< $< > $@
