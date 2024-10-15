# Analysis of the gut microbiome following dermal injury

## **Overview**
This repository holds the Jupyter notebooks which were used to generate Figure 3 for the analysis of our manuscript: 

**_Dermal injury drives a skin-gut axis that disrupts the intestinal microbiome and intestinal immune homeostasis_** (Published in Nature Communications).

**Authors:** Tatsuya Dokoshi<sup>1</sup>, Yang Chen<sup>1,2</sup>, Kellen J. Cavagnero<sup>1</sup>, Gibraan Rahman<sup>2</sup>, Daniel Hakim<sup>2</sup>, Samantha Brinton<sup>1</sup>, Hana Schwarz<sup>1</sup>, Alan O'Neill<sup>1</sup>, Yoshiyuki Nakamura<sup>1</sup>, Fengwu Li<sup>1</sup>, Nita H. Salzman<sup>3</sup>, Rob Knight<sup>4,5,6,7</sup>, Richard L. Gallo<sup>†</sup>

**Affiliations:**	

<sup>1</sup>Department of Dermatology, University of California, San Diego, La Jolla, CA 92037, United States.  
<sup>2</sup>Department of Pediatrics, University of California, San Diego, La Jolla, CA 92037, United States.  
<sup>3</sup>Department of Pediatrics, Division of Gastroenterology and Center for Microbiome Research, Medical College of Wisconsin, Milwaukee, WI.  
<sup>4</sup>Department of Pediatrics, University of California, San Diego, La Jolla, CA 92037, United States.  
<sup>5</sup>Department of Computer Science & Engineering, University of California, San Diego, La Jolla, CA 92037, United States.  
<sup>6</sup>Department of Bioengineering, University of California, San Diego, La Jolla, CA 92037, United States.  
<sup>7</sup>Center for Microbiome Innovation, University of California, San Diego, La Jolla, CA 92037, United States.

<sup>†</sup>Corresponding author

**Abstract:** 

The composition of the microbial community in the intestine influences the functions of distant organs such as the brain, lung, and skin. These microbes can promote disease or have beneficial functions, leading to the hypothesis that microbes in the gut explain the co-occurrence of intestinal and skin diseases. Here, we show that the reverse can occur, and that skin directly alters the gut microbiome. Disruption of the dermis by skin wounding or the digestion of dermal hyaluronan results in increased expression in the colon of antimicrobial genes Reg3 and Muc2 and changed the composition and behavior of remaining intestinal bacteria. Enhanced expression Reg3 and Muc2 was induced in vitro by exposure to hyaluronan released by these skin interventions. The change in the colon microbiome after skin wounding was functionally important as these bacteria penetrated the intestinal epithelium and enhanced colitis from dextran sodium sulfate (DSS) as shown by the ability to rescue skin associated DSS colitis with oral antibiotics, in germ-free mice, and fecal microbiome transplantation to unwounded mice from mice with skin wounds. These observations provide direct evidence of a skin-gut axis by demonstrating that damage to the skin disrupts homeostasis in intestinal host defense and alters the gut microbiome.

## **Data Availability**

Raw metagenomic sequencing data and corresponding metadata can be found on NCBI Sequence Read Archive (SRA) under BioProject ID [PRJNA1003965](https://submit.ncbi.nlm.nih.gov/subs/sra/SUB13748012/overview). Additionally, the data can also be found on Qiita under Study ID [14365](https://qiita.ucsd.edu/study/description/14365).

## **Data Processing**

All sequencing data was processed using the [Qiita default metagenomic workflow](https://github.com/qiita-spots/qp-knight-lab-processing). 

1. Adaptor and host filtering were performed with [qp-fastp-minimap2](https://github.com/qiita-spots/qp-fastp-minimap2). 
2. Filtered sequence files were aligned against reference database [WoL](https://biocore.github.io/wol/) using [Bowtie2](https://github.com/BenLangmead/bowtie2) with the [Woltka Qiita Plugin](https://github.com/qiita-spots/qp-woltka) for performing alignments. 
3. Resultant alignment files were processed using [Woltka](https://github.com/qiyunzhu/woltka) for taxonomic and functional predictions and feature table generation.

## **Data Filtering and Analyses**

1. Taxonomic feature tables were then further filtered using [Zebra Filter](https://github.com/biocore/zebra_filter) based on [genome coverage](https://pubmed.ncbi.nlm.nih.gov/36073806/) with default 10% minimum coverage threshold. Genomes falling below coverage threshold were removed from Woltka generated taxonomic feature table. 
2. Community (alpha and beta) analyses were performed by calculating the [Shannon Index](http://scikit-bio.org/docs/latest/generated/skbio.diversity.alpha.shannon.html) via Python's `skbio.diversity` package for alpha diversity and  phylogenetically informed robust Aitchison principal components analysis [(Phylo-RPCA)](https://github.com/biocore/gemelli) via Gemelli for beta diversity. (See Jupyter notebooks for specifics.)
3. Differential abundance analysis for taxonomic and function feature tables were performed using [Songbird](https://github.com/biocore/songbird).

## **Repository overview**
This repository contains the data inputs and Jupyter notebooks to generate Figure 3 in our manuscript. 
* `./data/`: All data inputs  
* `./reference/`: Reference (Gene Ontology and taxonomic mapping files)
* `./notebooks/`: Notebooks used to generate each of the plots
* `./plots/`: PNG files of plots generated
