# MINI-EX example

This folder contains an example of input and output files used to run MINI-EX.  

The [INPUTS folder](INPUTS/) contains:  
 
- **miniexExample_matrix.txt**: a reduced gene-to-count matrix containing 1500 genes and 1542 cells  
- **miniexExample_allMarkers.txt**: the output of Seurat FindAllMarkers filtered for genes present in the reduced expression matrix  
- **miniexExample_cell2clusters.txt**: the file containing the identity of each cell present in the reduced expression matrix  
- **miniexExample_identities.txt**: the file containing the identity of each cell cluster  
- **TF_list.txt**: the file containing 1879 Arabidopsis TFs  
- **GOIwant.txt**: (optional, it can be set to null) the file containing terms related to the regulons's expected functions  
- **miniexExample_grnboost2.txt**: (optional, it is set to null by default) if GRNBoost2, or another expression-based network, was already run, the output can be provided here     
  
  
  
The [OUTPUTS folder](OUTPUTS/) contains four sub-folders:   
- **GRNBoost2_output** containing the output of GRNBoost2  
- **GOenrichment_output** containing the output of the functional enrichment of the inferred regulons    
- **regulons_output** containing three files:  
	- miniexExample_TF_info_file.txt, a tab-separated file containing, for each TF, information about the TF's expression, whether it was retained or not in the final regulons list, and if not, at which step it was discarded. It also reports the percentage of cells for each cluster expressing the TF. This can be useful for adjusting the **expressionFilter** parameter in the last block of the [config file](https://github.com/VIB-PSB/MINI-EX/tree/main/docs/configuration.md).         
	- miniexExample_regulons.txt, a tab-separated file with TF, cell cluster and list of TGs for each of the inferred regulons  
	- miniexExample_rankedRegulons.xlsx, an excel file containing metadata for each of the inferred regulons. The different columns are explained below:    
		- TF: TF gene name (i.e. AT1G71930) 
		- alias: TF alias (i.e. VND7)  
		- hasTFrelevantGOterm: 'relevant_known_TF' if the TF is associated to a relevant GO term (relative to [GOsIwant.txt](https://github.com/VIB-PSB/MINI-EX/tree/main/example/INPUTS/GOsIwant.txt)), 'known_TF' if the TF is associated to another experimentally validated and/or manually curated GO term, 'unknown_TF' when the TF is uncharacterized   
		- GO: the GO term(s) the TF is associated with     
		- GOdescription: the description of the GO term(s) associated with the TF  
		- cluster: the cell cluster the TF acts in    
		- celltype:  the identity of the cell cluster the TF acts in    
		- isTF_DE: 1 if the TF is upregulated in the cell cluster it acts in, 0 if the TF is expressed (by at least 10% of the cells within the cell cluster) in the cell cluster it acts in    
		- totRegInCluster: number of total regulons within the cell cluster     
		- #TGs: number of TGs controlled by the regulon    
		- qval_cluster: FDR-corrected p-value of cell cluster enrichment (cluster specificity)    
		- closeness: closeness-centrality  
		- betweenness: betweenness-centrality    
		- GO_enrich_qval: FDR-corrected p-value of functional enrichment of the regulon's TGs (functional specificity - reporting only the lowest p-value among the relevant terms)  
		- GO_enrich_term: the relevant GO term (relative to [GOsIwant.txt](https://github.com/VIB-PSB/MINI-EX/tree/main/example/INPUTS/GOsIwant.txt)) for which the regulon's TGs showed the most significant enrichment    
		- GO_enrich_desc: description of the GO term for which the regulon's TGs showed the most significant enrichment    
		- #TGs_withGO: number of TGs enriched for the most significant relevant GO term    
		- borda_rank: global Borda ranking of the regulon  
		- borda_clusterRank: cluster-specific Borda ranking of the regulon  
		
- **figures** containing the three default figures MINI-EX produces:  
	- miniexExample_clustermap.svg, a clustermap showing the number of TGs per TF (y-axis) across the different single cell clusters (x-axis)   
	   
	![miniexExample_clustermap.svg](OUTPUTS/figures/miniexExample_clustermap.svg)
	- miniexExample_heatmapSpecificity.svg, a clustermap reporting the specificity of expression of the top 150 regulons across the different single cell clusters. Each TF is color coded accoring to the GO terms associated to it, in green for 'relevant_known_TF', in yellow for 'known_TF', and gray for 'unknown_TF'  
	  
	![miniexExample_heatmapSpecificity.svg](OUTPUTS/figures/miniexExample_heatmapSpecificity.svg)
	- miniexExample_heatmapDEcalls.svg, a clustermap reporting whether the top 150 TFs are upregulated (blue) or just expressed (by at least 10% of the cells within the cell cluster - white) in the cell cluster they act. Each TF is color coded accoring to the GO terms associated to it, in green for 'relevant_known_TF', in yellow for 'known_TF', and gray for 'unknown_TF'    
	  
	![miniexExample_heatmapDEcalls.svg](OUTPUTS/figures/miniexExample_heatmapDEcalls.svg)
		