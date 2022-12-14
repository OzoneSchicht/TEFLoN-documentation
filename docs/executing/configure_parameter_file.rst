=====================
Config parameter file
=====================

 Les fichiers de configurations permettent de dire à TEFLoN2 ce qu'il doit utiliser.
 TEFLoN2 à deux fichier de configuration : 

 * Le configuration du workflow
 * La confuguration des instuction cluster

Configuration of TEFLoN2
------------------------

TEFLoN2 uses Snakemake to perform its analyses. You have then first to provide your parameters in a .yaml file (see an example in the config.yaml file). Parameters are :

.. code-block:: yaml

    #all path can be relatif or absolute


    DEPENDANCES:
        PYTHON3:    "/path/to/python3" #[required] path to python 3 executable 
        BWA:    "path/to/bwa" #[required] path to bwa executable 
        SAMTOOLS:    "path/to/samtools" #[required] path to samtools executable 
        REPEATMASKER:    "path/to/repeatmasker" #[requiered if prep_custom] path to repeatmasker executable

    DATA:
        GENOME:    "name_reference_file.fasta" #[required] name of reference file in data_input/reference
        ANNOTATION:    "name_annotation_file.bed" #[required if prep_annotation] name of annotation file in data_input/library
        LIBRARY:    "name_TE_library.fasta" #[required if prep_custom][optional if prep_annotation] name of TE library file for your organism in data_input/library
        HIERARCHY:    "name_TE_hirarchiy.txt" #[requiered if prep_annotation] name of TE hirarchy file in data_input/library

    PARAMS:
        GENERAL:
        WORKING_DIRECTORY:    "" #[optional] path to working directory. Default: in the current directory
            PREFIX:    "name_run" #[required] name of run
        PREP_CUSTOM:
            CUTOFF:    "" #[optional] SW cutoff score for RepeatMasker, default=250 
            MIN_LENGTH:    "" #[optional] minimum length for RepeatMasker-predicted TE to be reported in the final annotation, default=200 
            SPLIT_DIST:    "" #[optional] minimum length for RepeatMasker-predicted TE to be reported in the final annotation, default=200 
            DIVERGENCE:    "" #[optional] only those repeats < x percent diverged from the consensus seq will be included in final annotation, default=20 
        DISCOVER:
            LEVEL_HIERARCHY1:    "family" #[required] level of the hierarchy file to guide initial TE search. #NOTE: It is recommended that you use the lowest level in the hierarchy file (i.e. "family" for data without a user-curated hierarchy)
            LEVEL_HIERARCHY2:    "order" #[required] level of the hierarchy to group similar TEs.    #NOTE: This must be either the same level of the hierarchy used in -l1 or a higher level (clustering at higher levels will reduce the number of TE instances found, but improve accuracy for discriminating TE identity)
            QUALITY:    "20" #[required] map quality threshold #NOTE: Mapped reads with map qualities lower than this number will be discarded
            EXCLUDE:    "" #[optional] newline separated file containing the name of any TE families to exclude from analysis #NOTE: Use same names as in column one of the hierarchy file
            STANDARD_DEVIATION:    "" #[optional] insert size standard deviation #NOTE: Used to manually override the insert size StdDev identified by samtools stat (check this number in the generated stats.txt file to ensure it seems more or less correct based on knowledge of sequencing library!)
            COVERAGE_OVERRIDE:    "" #[optional] coverage override #Note: Used to manually override the coverage estimate if you get the error: "Warning: coverage could not be estimated"
        COLLAPSE:
            THREASHOLD_SAMPLE:    "1" #[required] TEs must be supported by >= n reads in at least one sample
            THREASHOLD_ALL:    "1" #[required] TEs must be supported by >= n reads summed across all samples
            COVERAGE_OVERRIDE:    "" #[optional] coverage override #Note: Used to manually override the coverage estimate if you get the error: "Warning: coverage could not be estimated"
            QUALITY:    "20" #[required] map quality threshold
        COUNT:
            QUALITY:    "20" #[required] map quality threshold
        GENOTYPE:
            THREASHOLD_LOWER:    "1" #[optinal] sites genotyped as -9 if adjusted read counts lower than this threshold, default=1
            THREASHOLD_HIGHER :    "100" #[optinal] sites genotyped as -9 if adjusted read counts higher than this threshold, default=mean_coverage + 2*STDEV
            DATA_TYPE :    "pooled" #[required] must be either haploid, diploid, or pooled #NOTE: haplid/diploid genotyper under construction, all types must use pooled

Config Cluster
--------------