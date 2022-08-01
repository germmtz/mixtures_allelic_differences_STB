# mixtures_allelic_richness_STB

Data and code used for the study : "From cultivar mixtures to allelic mixtures: opposite effects of allelic richness between genotypes and genotype richness in wheat".

The script "Manuscript_Analyses.R" contains all code for the statistical analysis presented in the manuscript (main text & supplementary information). This script uses files produced in the folder "Locus-by-locus analysis" as inputs, and "manhattan_custom.R" as a source function ("manhattan_custom.R" is used to highlight SNPs in a given interval and to write specified SNPs name on manhattan plots). The file "Traits_monocultures.csv" contains the 20 functional traits measured on the 179 monoculture plots (see Supplementary Methods for more information on trait measurement). This file is used as an input in the script "Manuscript_Analyses.R".

The "Locus-by-locus analysis" folder contains all analyses conducted to test the effect of allelic richness on the four variables of interest: Grain Yield (GY, g/m²), Spike Number per m² (SNb, nb spikes/m²), Thousand Kernel Weight (TKW, g), and Septoria tritici blotch (STB) severity. The locus-by-locus analysis is performed with the script "Allelic_richness_locus_by_locus_analysis.R". This analysis generates a list of .csv files with one file per chromosome. Each file contains the pvalues and estimated effect sizes of the tested SNPs for the given chromosome. These output files are stored in folders named after the variables for which the effect of allelic richness was tested ("RAW_GY", "RAW_SNb", "RAW_TKW", and "RAW_severity"). The script "Allelic_richness_locus_by_locus_output_processing.R" combines all .csv files into a single dataframe and produces three diagnostic plots: Manahattan plots, histograms of p-value distributions, and p-value q-q plots. p-value thresholds were computed based on a Family-Wise Error Rate of 5% using the Galwey correction. This is done in the "pvalue_thresholds" folder with the "Meff_computation.R" script. "Meff_computation.R" uses the "Meff_function.R" as a source function and generates "GY_thresholds.csv" and "STB_thresholds.csv" as outputs (these files contains different thresholds computed according to different methods but we only retained the Galwey method (most recent) for the analyses. Since GY, SNb, and TKW were analyzed with the same number of SNPs (~19K), we used the same significance threshold for the three variables ("GY_thresholds.csv"), whereas we computed a different thresholds for STB ("STB_thresholds.csv") for which we could only include ~6K SNPs in the analysis. The "geno_pos.csv" file contains the physical positions of the SNPs.

Upstream the locus-by-locus analysis, phenotypic and genotypic files are prepared in the "Phenoytpic file preparation" and "Genotypic file preparation" folders, respecively.

The phenotypic file preparation includes the correction of yield-related variables (GY, SNb, and TKW) for spatial auto-correlation in the "Spatial_analyses_YLD_variables" folder, and the computation of plot-level variables from individual-level variables with the "Allelic_richness_phenotypic_file_prep.R" script. In this script, we compute both absolute plot values (termed "RAW_...) and relative plot values (termed "RYT_..., only for mixture plots). All phenotypic files have the same structure with the same first 6 columns: "focal" = identity of the focal genotype (the one for which the variable is measured, only relevant for variables measured at the individual-level), "neighbor" = identity of the neighbor genotype (the neighbor of the genotype for which the variable is measured, only relevant for variables measured at the individual-level), "pair" = identity of the genotypic pair (combines the identity of the focal and the neighbor genotypes), "assoc" = type of plot ("M" = monoculture or pure stand plot, "P" = mixture plot), "row" = position of the plot along the smallest dimension of the grid (see Figure 1), "column" = position of the plot along the largest dimension of the grid (see Figure 1).

The genotypic file preparation is done with the "Allelic_richness_genotypic_file_prep.R" script and includes SNP filtering, computation of matrices of allelic richness, and computation of matrices of genetic similarity between genotypic pairs. The analysis is done separatly for yield-related variables and for STB severity since the two types of variable were not measured on the same set of plots.
