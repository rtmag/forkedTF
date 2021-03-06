# forkedTF
forkedTF is an R-library that generates Forked-PMW (FPMW) and Forked-Sequence Logos (F-Logos) for a better depiction of the sequence affinity (DNA sequence and DNA methylation level) of a TF of interest together with those of a segregated list of partners. Indeed, in contrast to current methods that aggregate binding sites of dimer TFs into a single PWM/logo, FPWM and F-Logo represent dimer partner PWM and sequence logos as forked from the main TF motif. Consequently, forkedTF improves PWM models of TF dimers, thereby enhancing our understanding of TF cooperativity, and opens a novel avenue for accurate TFBS prediction.
 
### Current version: 0.1.0
### Installation
Type the following in R console:
```r
install.packages("devtools")
library("devtools")
devtools::install_github("https://github.com/benoukraflab/forkedTF")
```
#### Dependencies
   - [TFregulomeR](https://github.com/benoukraflab/TFregulomeR) (>= 1.2)
   - [ggplot2](https://cran.r-project.org/web/packages/ggplot2/index.html) (>= 3.3.0)
   - [gridExtra](https://cran.r-project.org/web/packages/gridExtra/index.html) (>= 2.3)
   - [gridGraphics](https://cran.r-project.org/web/packages/gridGraphics/index.html) (>= 0.4.1)
   - [ggseqlogo](https://cran.r-project.org/web/packages/ggseqlogo/index.html) (>= 0.1)
   - [cowplot](https://cran.r-project.org/web/packages/cowplot/index.html) (>= 1.0.0)
   - [grid](https://www.rdocumentation.org/packages/grid/versions/3.6.1) (>= 3.6.1)

## Documentation
A detailed description of all forkedTF's features is available [here](http://benoukraf-lab.com/vignettes/vignette-FPWM.html).

## Quick usage
#### MiniCofactor Report
This function helps in the exploration of binding partners in a cell line. Input the `mainTF`, `cell` line of interest and the `cobinding_threshold` to generate a PDF report of the binding partners.

```r
library("forkedTF")
miniCofactorReport( TF = "CEBPB", cell = "K562",cobinding_threshold=.06)
```
<div align="center">
<a name="miniCofactorReport"/>
<img src="./inst/MM1_HSA_K562_CEBPB_cofactor_minireport.png" alt="miniCofactorReport" width="490" height="630" ></img>
</a>
</div>

#### FPWM creation and plot
Use the `createFPWM` function to extract the motif, from empirical datasets, that a TF uses when binding with a partner TF. `plotFPWM` helps in visualizing the FPWM.
```r
fpwm <- createFPWM(mainTF ="CEBPB",
                        partners = c("ATF4","ATF7","ATF3","JUND","FOS","CEBPD"),
                        cell = "K562", 
                        forkPosition = 5,
                        flipMatrix = FALSE)

plotFPWM(fpwm,pdfName="fpwm_plot.pdf")
```
<div align="center">
<a name="fpwm_plot"/>
<img src="./inst/fpwm_plot.png" alt="fpwm_plot" width="340" height="630" ></img>
</a>
</div>

#### Writing FPWM
Save the FPWM to a local file can be used in matrix scanning or matrix clustering in `transfact` format or `FPWMtransfact` format. `Transfact` format will have a matrix for each interacting partner in the FPWM, while `FPWMtransfact` will output a single matrix.
```r
write.FPWM(FPWM = fpwm, format = "transfac", fileName = "FPWM.transfact" )
write.FPWM(FPWM = fpwm, format = "FPWMtransfac", fileName = "FPWM.FPWMtransfac" )
```
## Contributors
   - Roberto Tirado-Magallanes
   - Aida Ghayour-Khiavi
   - Quy Xiao Xuan Lin
   - Touati Benoukraf

## License
This project is licensed under GNU General Public License - see [LICENSE.txt](./LICENSE.txt) for details.
