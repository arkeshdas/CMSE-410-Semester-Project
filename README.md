# False Discovery Rate Methods in an Immune Response GWAS

This project compares multiple-testing correction methods on GWAS summary statistics from the Milieu Interieur immune response cohort. The analysis focuses on how raw p-value signals change after applying Bonferroni-style family-wise correction, Benjamini-Hochberg, Benjamini-Yekutieli, Benjamini-Krieger-Yekutieli, and Storey-Tibshirani q-values.

The final report is built from `Arkesh_Das_CMSE_410_Semester_Project.Rmd` and includes Manhattan plots, QQ plots, adjusted p-value plots, and a short interpretation of the strongest chromosome 6 signal.

## Outputs

- `Arkesh_Das_CMSE_410_Semester_Project.pdf` - polished report for portfolio review
- `Arkesh_Das_CMSE_410_Semester_Project.html` - browser-readable version of the report
- `Arkesh_Das_CMSE_410_Semester_Project_files/figure-latex/` - regenerated PDF plot assets used by the report

## Data

The raw GWAS summary-statistics file is about 395 MB, so it is intentionally not committed to git. The repository expects the file to be available as:

```text
HBV_HBc_GWAS_serostatus.txt
```

That filename is already ignored in `.gitignore`, which keeps the local data available for rendering without pushing it to GitHub.

To reproduce the report, either place the file in the project root:

```bash
cp "/path/to/HBV_HBc_GWAS_serostatus.txt" ./HBV_HBc_GWAS_serostatus.txt
```

or point the report to another location:

```bash
GWAS_DATA_PATH="/path/to/HBV_HBc_GWAS_serostatus.txt" Rscript -e "rmarkdown::render('Arkesh_Das_CMSE_410_Semester_Project.Rmd')"
```

For a public portfolio repository, the best data-sharing option is to attach `HBV_HBc_GWAS_serostatus.txt` as a GitHub Release asset or provide the original GWAS Catalog download link in this section. Git LFS would also work, but it adds setup and bandwidth constraints for anyone cloning the project.

## Reproducing the Report

Install R and the required packages:

```r
install.packages(c("rmarkdown", "knitr", "tidyverse", "BiocManager"))
BiocManager::install("qvalue")
```

Pandoc is required by `rmarkdown`. If it is not already installed, install it through RStudio, Quarto, or a package manager such as conda.

Render the PDF report:

```bash
Rscript -e "rmarkdown::render('Arkesh_Das_CMSE_410_Semester_Project.Rmd', output_format = 'pdf_document')"
```

Render the HTML report:

```bash
Rscript -e "rmarkdown::render('Arkesh_Das_CMSE_410_Semester_Project.Rmd', output_format = 'html_document')"
```

## Project Notes

The report uses a 100,000-SNP reproducible sample for method comparison and checks the full filtered dataset for the strongest raw association. The main takeaway is that apparent GWAS discoveries depend strongly on the multiple-testing method, and candidate biological interpretation should be tied to corrected significance, genome build, and variant annotation.
