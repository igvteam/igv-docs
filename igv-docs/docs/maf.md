**MAF** (mutation annotation format) **files display mutations**. IGV recognizes text-based files with .maf, .maf.txt  file extensions as mutation files.

IGV will visualize each individual sample's mutation data as a single track.

![](img/SL_IGV_MAF_color2015-02-18%2013.45.48.png)

*   The _all chromosomes_ view summarizes mutations in a coverage track (**Screenshot below**, 2015.02.18).
*   Zooming in, individual chromosome views and more detailed views mark sites of mutations with open rectangles. Default settings display these in black-and-white.
*   **Color code mutations** by mutation type (**Screenshot above**, 2015.02.18) by checking the _Color code mutations_ box under _View_\>_Preferences_\>_Mutations_. See the [Preferences page](http://www.broadinstitute.org/software/igv/Preferences#Mutations) for more details.
*   Mouse-over or click on a mutation to bring up an information panel on the specific mutation. This panel displays the information provided in the mutation file columns, in order, up to an area limit.
*   A site where both alleles are mutated, or is mutated in multiple samples in a track that is a conglomerate of multiple samples, displays the rectangle with a horizontal line through the middle.

![](img/IGV_MAF_all_2015-02-18%2012.03.21.png)