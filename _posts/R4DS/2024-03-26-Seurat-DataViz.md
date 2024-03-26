---
layout: post
title: Data visualization methods in Seurat
subtitle: Day 7. Data visualization with Seurat
tags: [R, Data Science, Data Visualisation, Genomics]
comments: true
categories: R DataScience DataViz
author: Chí Trung HÀ
---


```R
library(Seurat)
library(SeuratData)
library(ggplot2)
library(patchwork)
pbmc3k.final <- LoadData("pbmc3k", type = "pbmc3k.final")
pbmc3k.final$groups <- sample(c("group1", "group2"), size = ncol(pbmc3k.final), replace = TRUE)
features <- c("LYZ", "CCL5", "IL32", "PTPRCAP", "FCGR3A", "PF4")
pbmc3k.final
```

## Five visualizations of marker feature expression


```R
# 1. Ridge plots - from ggridges. Visualize single cell expression distributions in each cluster
options(repr.plot.width = 18, repr.plot.height = 12)
RidgePlot(pbmc3k.final, features = features, ncol = 2)
```
    
![png](/assets/img/Seurat-DataViz_files/Seurat-DataViz_3_1.png)
    



```R
# 2. Violin plot - Visualize single cell expression distributions in each cluster
VlnPlot(pbmc3k.final, features = features)
```


    
![png](/assets/img/Seurat-DataViz_files/Seurat-DataViz_4_0.png)
    



```R
# 3. Feature plot - visualize feature expression in low-dimensional space
FeaturePlot(pbmc3k.final, features = features)
```


    
![png](/assets/img/Seurat-DataViz_files/Seurat-DataViz_5_0.png)
    



```R
# 4. Dot plots - the size of the dot corresponds to the percentage of cells expressing the
# feature in each cluster. The color represents the average expression level
DotPlot(pbmc3k.final, features = features) + RotatedAxis()
```


    
![png](/assets/img/Seurat-DataViz_files/Seurat-DataViz_6_0.png)
    



```R
# 5. Single cell heatmap of feature expression
DoHeatmap(subset(pbmc3k.final, downsample = 100), features = features, size = 3)
```


    
![png](/assets/img/Seurat-DataViz_files/Seurat-DataViz_7_0.png)
    


## New additions to FeaturePlot


```R
# Plot a legend to map colors to expression levels
FeaturePlot(pbmc3k.final, features = "MS4A1")
```


    
![png](/assets/img/Seurat-DataViz_files/Seurat-DataViz_9_0.png)
    



```R
# Adjust the contrast in the plot
FeaturePlot(pbmc3k.final, features = "MS4A1", min.cutoff = 1, max.cutoff = 3)
```


    
![png](/assets/img/Seurat-DataViz_files/Seurat-DataViz_10_0.png)
    



```R
# Calculate feature-specific contrast levels based on quantiles of non-zero expression.
# Particularly useful when plotting multiple markers
FeaturePlot(pbmc3k.final, features = c("MS4A1", "PTPRCAP"), min.cutoff = "q10", max.cutoff = "q90")
```


    
![png](/assets/img/Seurat-DataViz_files/Seurat-DataViz_11_0.png)
    



```R
# Visualize co-expression of two features simultaneously
FeaturePlot(pbmc3k.final, features = c("MS4A1", "CD79A"), blend = TRUE)
```


    
![png](/assets/img/Seurat-DataViz_files/Seurat-DataViz_12_0.png)
    



```R
# Split visualization to view expression by groups (replaces FeatureHeatmap)
FeaturePlot(pbmc3k.final, features = c("MS4A1", "CD79A"), split.by = "groups")
```


    
![png](/assets/img/Seurat-DataViz_files/Seurat-DataViz_13_0.png)
    


## Updated and expanded visualization functions
In addition to changes to `FeaturePlot()`, several other plotting functions have been updated and expanded with new features and taking over the role of now-deprecated functions


```R
# Violin plots can also be split on some variable. Simply add the splitting variable to object
# metadata and pass it to the split.by argument
VlnPlot(pbmc3k.final, features = "percent.mt", split.by = "groups")
```


    
![png](/assets/img/Seurat-DataViz_files/Seurat-DataViz_15_0.png)
    



```R
# SplitDotPlotGG has been replaced with the `split.by` parameter for DotPlot
DotPlot(pbmc3k.final, features = features, split.by = "groups") + RotatedAxis()
```


    
![png](/assets/img/Seurat-DataViz_files/Seurat-DataViz_16_0.png)
    



```R
# DimPlot replaces TSNEPlot, PCAPlot, etc. In addition, it will plot either 'umap', 'tsne', or
# 'pca' by default, in that order
DimPlot(pbmc3k.final)
```


    
![png](/assets/img/Seurat-DataViz_files/Seurat-DataViz_17_0.png)
    



```R
pbmc3k.final.no.umap <- pbmc3k.final
pbmc3k.final.no.umap[["umap"]] <- NULL
DimPlot(pbmc3k.final.no.umap) + RotatedAxis()
```


    
![png](/assets/img/Seurat-DataViz_files/Seurat-DataViz_18_0.png)
    



```R
# DoHeatmap now shows a grouping bar, splitting the heatmap into groups or clusters. This can
# be changed with the `group.by` parameter
DoHeatmap(pbmc3k.final, features = VariableFeatures(pbmc3k.final)[1:100], cells = 1:500, size = 4,
    angle = 90) + NoLegend()
```


    
![png](/assets/img/Seurat-DataViz_files/Seurat-DataViz_19_0.png)
    


## Applying themes to plots
With Seurat, all plotting functions return ggplot2-based plots by default, allowing one to easily capture and manipulate plots just like any other ggplot2-based plot.


```R
baseplot <- DimPlot(pbmc3k.final, reduction = "umap")
# Add custom labels and titles
baseplot + labs(title = "Clustering of 2,700 PBMCs")
```


    
![png](/assets/img/Seurat-DataViz_files/Seurat-DataViz_21_0.png)
    



```R
# Seurat also provides several built-in themes, such as DarkTheme; for more details see
# ?SeuratTheme
baseplot + DarkTheme()
```


    
![png](/assets/img/Seurat-DataViz_files/Seurat-DataViz_22_0.png)
    



```R
# Chain themes together
baseplot + FontSize(x.title = 20, y.title = 20) + NoLegend()
```


    
![png](/assets/img/Seurat-DataViz_files/Seurat-DataViz_23_0.png)
    


## Interactive plotting features
Seurat utilizes R’s plotly graphing library to create interactive plots. This interactive plotting feature works with any ggplot2-based scatter plots (requires a geom_point layer). To use, simply make a ggplot2-based scatter plot (such as `DimPlot()` or `FeaturePlot()`) and pass the resulting plot to `HoverLocator()`


```R
# Include additional data to display alongside cell names by passing in a data frame of
# information.  Works well when using FetchData
plot <- FeaturePlot(pbmc3k.final, features = "MS4A1")
HoverLocator(plot = plot, information = FetchData(pbmc3k.final, vars = c("ident", "PC_1", "nFeature_RNA")))
```


Another interactive feature provided by Seurat is being able to manually select cells for further investigation. We have found this particularly useful for small clusters that do not always separate using unbiased clustering, but which look tantalizingly distinct. You can now select these cells by creating a ggplot2-based scatter plot (`such as with DimPlot()` or `FeaturePlot()`, and passing the returned plot to `CellSelector()`). `CellSelector()` will return a vector with the names of the points selected, so that you can then set them to a new identity class and perform differential expression.

For example, let’s pretend that DCs had merged with monocytes in the clustering, but we wanted to see what was unique about them based on their position in the tSNE plot.


```R
pbmc3k.final <- RenameIdents(pbmc3k.final, DC = "CD14+ Mono")
plot <- DimPlot(pbmc3k.final, reduction = "umap")
select.cells <- CellSelector(plot = plot)
```


    Error in RenameIdents.Seurat(pbmc3k.final, DC = "CD14+ Mono"): Cannot find any of the provided identities
    Traceback:


    1. RenameIdents(pbmc3k.final, DC = "CD14+ Mono")

    2. RenameIdents.Seurat(pbmc3k.final, DC = "CD14+ Mono")

    3. stop("Cannot find any of the provided identities")


We can then change the identity of these cells to turn them into their own mini-cluster.




```R
head(select.cells)
```






```R
Idents(pbmc3k.final, cells = select.cells) <- "NewCells"

# Now, we find markers that are specific to the new cells, and find clear DC markers
newcells.markers <- FindMarkers(pbmc3k.final, ident.1 = "NewCells", ident.2 = "CD14+ Mono", min.diff.pct = 0.3,
    only.pos = TRUE)
head(newcells.markers)
```


    Error in WhichCells.Seurat(object = object, idents = ident.1): Cannot find the following identities in the object: NewCells
    Traceback:


    1. FindMarkers(pbmc3k.final, ident.1 = "NewCells", ident.2 = "CD14+ Mono", 
     .     min.diff.pct = 0.3, only.pos = TRUE)

    2. FindMarkers.Seurat(pbmc3k.final, ident.1 = "NewCells", ident.2 = "CD14+ Mono", 
     .     min.diff.pct = 0.3, only.pos = TRUE)

    3. IdentsToCells(object = object, ident.1 = ident.1, ident.2 = ident.2, 
     .     cellnames.use = cellnames.use)

    4. WhichCells(object = object, idents = ident.1)

    5. WhichCells.Seurat(object = object, idents = ident.1)

    6. stop("Cannot find the following identities in the object: ", 
     .     paste(idents[!idents %in% levels(x = Idents(object = object))], 
     .         sep = ", "))



```R
pbmc3k.final <- CellSelector(plot = plot, object = pbmc3k.final, ident = "selected")
```

    
    Listening on http://127.0.0.1:7339
    
    Warning message:
    "Cannot find cells provided"



    
![png](/assets/img/Seurat-DataViz_files/Seurat-DataViz_31_1.png)
    



```R
levels(pbmc3k.final)
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>'CD14+ Mono'</li><li>'Naive CD4 T'</li><li>'Memory CD4 T'</li><li>'B'</li><li>'CD8 T'</li><li>'FCGR3A+ Mono'</li><li>'NK'</li><li>'Platelet'</li></ol>



## Plotting Accessories
Along with new functions add interactive functionality to plots, Seurat provides new accessory functions for manipulating and combining plots.


```R
# LabelClusters and LabelPoints will label clusters (a coloring variable) or individual points
# on a ggplot2-based scatter plot
plot <- DimPlot(pbmc3k.final, reduction = "pca") + NoLegend()
LabelClusters(plot = plot, id = "ident")
```


    
![png](/assets/img/Seurat-DataViz_files/Seurat-DataViz_34_0.png)
    



```R
# Both functions support `repel`, which will intelligently stagger labels and draw connecting
# lines from the labels to the points or clusters
LabelPoints(plot = plot, points = TopCells(object = pbmc3k.final[["pca"]]), repel = TRUE)
```

    When using repel, set xnudge and ynudge to 0 for optimal results
    



    
![png](/assets/img/Seurat-DataViz_files/Seurat-DataViz_35_1.png)
    


Plotting multiple plots was previously achieved with the `CombinePlot()` function. We are deprecating this functionality in favor of the patchwork system. Below is a brief demonstration but please see the patchwork package website here for more details and examples.


```R
plot1 <- DimPlot(pbmc3k.final)
# Create scatter plot with the Pearson correlation value as the title
plot2 <- FeatureScatter(pbmc3k.final, feature1 = "LYZ", feature2 = "CCL5")
# Combine two plots
plot1 + plot2
```


    
![png](/assets/img/Seurat-DataViz_files/Seurat-DataViz_37_0.png)
    



```R
# Remove the legend from all plots
(plot1 + plot2) & NoLegend()
```


    
![png](/assets/img/Seurat-DataViz_files/Seurat-DataViz_38_0.png)
    


Session Info


```R
sessionInfo()
```


    R version 4.3.2 (2023-10-31)
    Platform: aarch64-apple-darwin20 (64-bit)
    Running under: macOS Sonoma 14.3.1
    
    Matrix products: default
    BLAS:   /Library/Frameworks/R.framework/Versions/4.3-arm64/Resources/lib/libRblas.0.dylib 
    LAPACK: /Library/Frameworks/R.framework/Versions/4.3-arm64/Resources/lib/libRlapack.dylib;  LAPACK version 3.11.0
    
    locale:
    [1] C
    
    time zone: Australia/Brisbane
    tzcode source: internal
    
    attached base packages:
    [1] stats     graphics  grDevices utils     datasets  methods   base     
    
    other attached packages:
    [1] shiny_1.8.0             patchwork_1.2.0         ggplot2_3.5.0          
    [4] pbmc3k.SeuratData_3.1.4 SeuratData_0.2.2.9001   Seurat_5.0.0           
    [7] SeuratObject_5.0.1      sp_2.1-3               
    
    loaded via a namespace (and not attached):
      [1] matrixStats_1.2.0      spatstat.sparse_3.0-3  httr_1.4.7            
      [4] RColorBrewer_1.1-3     repr_1.1.6             tools_4.3.2           
      [7] sctransform_0.4.1      utf8_1.2.4             R6_2.5.1              
     [10] lazyeval_0.2.2         uwot_0.1.16            withr_3.0.0           
     [13] gridExtra_2.3          progressr_0.14.0       cli_3.6.2             
     [16] textshaping_0.3.7      spatstat.explore_3.2-6 fastDummies_1.7.3     
     [19] labeling_0.4.3         sass_0.4.9             spatstat.data_3.0-4   
     [22] ggridges_0.5.6         pbapply_1.7-2          systemfonts_1.0.5     
     [25] pbdZMQ_0.3-11          parallelly_1.37.1      generics_0.1.3        
     [28] ica_1.0-3              spatstat.random_3.2-3  crosstalk_1.2.1       
     [31] dplyr_1.1.4            Matrix_1.6-5           ggbeeswarm_0.7.2      
     [34] fansi_1.0.6            abind_1.4-5            lifecycle_1.0.4       
     [37] yaml_2.3.8             Rtsne_0.17             grid_4.3.2            
     [40] promises_1.2.1         crayon_1.5.2           miniUI_0.1.1.1        
     [43] lattice_0.21-9         cowplot_1.1.3          pillar_1.9.0          
     [46] future.apply_1.11.1    codetools_0.2-19       leiden_0.4.3.1        
     [49] glue_1.7.0             getPass_0.2-4          data.table_1.15.2     
     [52] vctrs_0.6.5            png_0.1-8              spam_2.10-0           
     [55] gtable_0.3.4           cachem_1.0.8           mime_0.12             
     [58] survival_3.5-7         ellipsis_0.3.2         fitdistrplus_1.1-11   
     [61] ROCR_1.0-11            nlme_3.1-163           RcppAnnoy_0.0.22      
     [64] bslib_0.6.1            irlba_2.3.5.1          vipor_0.4.7           
     [67] KernSmooth_2.23-22     colorspace_2.1-0       ggrastr_1.0.2         
     [70] tidyselect_1.2.1       compiler_4.3.2         plotly_4.10.4         
     [73] scales_1.3.0           lmtest_0.9-40          rappdirs_0.3.3        
     [76] stringr_1.5.1          digest_0.6.35          goftest_1.2-3         
     [79] spatstat.utils_3.0-4   htmltools_0.5.7        pkgconfig_2.0.3       
     [82] base64enc_0.1-3        fastmap_1.1.1          rlang_1.1.3           
     [85] htmlwidgets_1.6.4      farver_2.1.1           jquerylib_0.1.4       
     [88] zoo_1.8-12             jsonlite_1.8.8         magrittr_2.0.3        
     [91] dotCall64_1.1-1        IRkernel_1.3.2         munsell_0.5.0         
     [94] Rcpp_1.0.12            reticulate_1.35.0      stringi_1.8.3         
     [97] MASS_7.3-60            plyr_1.8.9             parallel_4.3.2        
    [100] listenv_0.9.1          ggrepel_0.9.5          deldir_2.0-4          
    [103] IRdisplay_1.1          splines_4.3.2          tensor_1.5            
    [106] igraph_2.0.3           uuid_1.2-0             spatstat.geom_3.2-9   
    [109] RcppHNSW_0.6.0         reshape2_1.4.4         evaluate_0.23         
    [112] httpuv_1.6.14          RANN_2.6.1             tidyr_1.3.1           
    [115] purrr_1.0.2            polyclip_1.10-6        future_1.33.1         
    [118] scattermore_1.2        xtable_1.8-4           RSpectra_0.16-1       
    [121] later_1.3.2            viridisLite_0.4.2      ragg_1.2.7            
    [124] tibble_3.2.1           memoise_2.0.1          beeswarm_0.4.0        
    [127] cluster_2.1.4          globals_0.16.3        

