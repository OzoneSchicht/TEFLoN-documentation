====================
Output files summary
====================

Here is the structure of the output files obtained after running the pipeline.


.. code-block:: none

	WORK_DIRECTORY/data_output_PREFIX/
	├── 0-reference
	│	├── PREFIX.prep_MP
	│	│	├── PREFIX.annotatedTE.fa
	│	│	├── PREFIX.mappingRef.fa
	│	│	├── PREFIX.mappingRef.fa.amb
	│	│	├── PREFIX.mappingRef.fa.ann
	│	│	├── PREFIX.mappingRef.fa.bwt
	│	│	├── PREFIX.mappingRef.fa.pac
	│	│	├── PREFIX.mappingRef.fa.sa
	│	│	└── PREFIX.pseudo.fa
	│	├── PREFIX.prep_TF
	│	│   ├── PREFIX.genomeSize.txt
	│	│   ├── PREFIX.hier
	│	│   ├── PREFIX.pseudo2ref.txt
	│	│   ├── PREFIX.ref2pseudo.txt
	│	│   └── PREFIX.te.pseudo.bed
	│	└── PREFIX.prep_RM          --------
	│	    ├── GENOME.fasta               |
	│	    ├── GENOME.fasta.align         |
	│	    ├── GENOME.fasta.cat.gz        |--- Specific to prepration custom 
	│	    ├── GENOME.fasta.masked        |
	│	    ├── GENOME.fasta.out           |
	│	    ├── GENOME.fasta.tbl           |
	│	    └── PREFIX.bed        ----------
	├── 1-mapping
	│	├── SAMPLE_NAME.sorted.bam
	│	├── SAMPLE_NAME.sorted.bam.bai
	│	├── SAMPLE_NAME.sorted.cov.txt
	│	├── SAMPLE_NAME.sorted.stats.txt
	│	├── SAMPLE_NAME.sorted.subsmpl.bam
	│	├── SAMPLE_NAME.sorted.subsmpl.bam.bai
	│	├── SAMPLE_NAME.sorted.subsmpl.cov.txt
	│	└── SAMPLE_NAME.sorted.subsmpl.stats.txt
	├── 3-countPos
	│	├── SAMPLE_NAME.all_positions_sorted.collapsed.txt
	│	├── SAMPLE_NAME.all_positions_sorted.txt
	│	├── SAMPLE_NAME.all_positions.txt
	│	├── SAMPLE_NAME.counts.txt
	│	├── SAMPLE_NAME.pseudoSpace.genotypes.txt
	│	├── union_sorted.collapsed.txt
	│	├── union_sorted.txt
	│	└── union.txt
	├── 4-genotypes
	│	└── SAMPLE_NAME.genotypes.txt
	└── sample_names.txt


Most useful output
------------------


.. csv-table:: Comparison
	:header: chr, 5' breakpoint, 3' breakpoint, Level 1,Level 2, Stand, Reference TE ID, 5' soft-clipped reads, 3' soft-clipped reads, Presence reads, Abscence reads, Ambiguous reads,Genotype,Identifier TE
	:widths: 15 10 30 30 30 30 30 30 30 30 30 30 30 30

	2R,38145,\-,gate,ltr,\-,\-,\+,\-,1,0,0,1.0,te01
	2R,38145,\-,rt1b,non-ltr,.,\-,\+,\-,1,0,0,1.0,te02
	2R,21076732,21077084,ine-1,helitron,\-,FBti0061454,\+,\-,2,0,0,1.0,te352




#. chromosome
#. 5' breakpoint estimate ("-" if estimate not available)
#. 3' breakpoint estimate ("-" if estimate not available)
#. search level id (Usually TE family)
#. cluster level id (Usually TE order or class)
#. strand ("." if strand could not be detected)
#. reference TE ID ("-" if novel insertion)
#. 5' breakpoint is supported by soft-clipped reads (if TRUE "+" else "-")
#. 3' breakpoint is supported by soft-clipped reads (if TRUE "+" else "-")
#. read count for "presence reads"
#. read count for "absence reads"
#. read count for "ambiguous reads"
#. genotype for every TE (allele frequency for pooled data, present/absent for haploid, present/absent/heterozygous for diploid) #Note: haploid/diploid caller is under construction, use "pooled" for presence/absence read counts
#. numbered identifier for each TE in the population




