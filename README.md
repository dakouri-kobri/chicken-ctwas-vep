# Chicken cTWAS Fine Mapping and Variant Annotation

A reproducible functional genomics practical using **R**, **Quarto**,
**renv**, and **Git** to prioritize candidate genes and SNPs in chicken
trait-associated regions and investigate their functional annotations.

This is my version of one the computer exercise sessions done as part of the course of [Genome analysis BK0003 HT2026, 15 ECT credits](https://www.slu.se/en/student-web/studies/courses-and-programmes/course-search/kurser/g/genome-analysis/), at SLU (Swedish University of Agricultural Sciences), Uppsala, Sweden, autumn 2026

## Project objectives

- Analyze candidate regions using causal transcriptome-wide association
  analysis (cTWAS).
- Compare results obtained with uniform and empirically estimated group priors.
- Examine how joint fine mapping prioritizes genes and SNPs.
- Annotate selected SNPs using Ensembl Variant Effect Predictor (VEP).
- Interpret statistical support alongside predicted functional consequences.

## Data

The practical uses chicken genotype, gene-expression, and GWAS data
provided with the course materials. The study populations are feral
chickens from Hawaii and Bermuda.

The analysis uses 375 individuals matched between the genotype and
expression datasets.

Input files and preprocessing steps are documented in the Quarto report.

## Analysis workflow

### 1. Prepare and validate the inputs

Inspect identifiers, match genotype and expression samples, and prepare
the GWAS information required by the analysis.

### 2. Run cTWAS with uniform priors

Perform the first analysis pass and obtain posterior inclusion
probabilities (PIPs) for candidate genes and SNPs.

### 3. Estimate group priors and rerun the analysis

Estimate empirical gene and SNP group weights from pass 1, then use
these weights in pass 2.

### 4. Compare fine-mapping results

Compare PIPs and leading candidates between passes.

Both passes assess genes and SNPs jointly. Accounting for correlated
signals can concentrate support on fewer candidates, although strongly
correlated candidates may remain difficult to distinguish.

### 5. Annotate selected SNPs with VEP

Select eight SNPs spanning higher and lower PIPs. Obtain their alleles
from the supplied genotype file and submit them to Ensembl VEP.

The VEP analysis uses the chicken **GRCg7b** assembly. Submission settings
and exported annotations are documented in the report.

### 6. Interpret the evidence

Compare fine-mapping support with VEP annotations and discuss whether
the annotations strengthen a plausible causal explanation or leave
substantial uncertainty.

## Main fine-mapping findings

After applying the empirical group weights:

- PIPs increased by 0.0061–0.0188 for the four candidate genes.
- Several SNP PIPs decreased slightly.
- The leading candidate remained unchanged in each of the four loci.

The leading genes in their respective loci remained
`ENSGALG00010008087` and `ENSGALG00010011018`. The leading SNPs in the
other two loci remained `1:76750239` and `4:78065006`.

Because the group weights were estimated using these same loci,
the pass 2 changes are not independent validation of the candidates.

## Interpretation and limitations

PIPs express posterior support under the fitted model and its
assumptions. They do not establish biological causality.

VEP predicts consequences relative to a reference assembly and its
annotations. A predicted consequence can inform a biological hypothesis,
but does not demonstrate that a variant affects the trait.

Variant coordinates, alleles, and reference assembly must be consistent
when interpreting annotations.

## Reproduce the analysis

### Requirements

- R
- Quarto CLI
- RStudio, recommended
- Access to the required course input files

R package versions are recorded in `renv.lock`. R and the Quarto CLI
must be installed separately.

### Restore the R environment

Open the RStudio project and run:

```r
renv::restore()
```

### Render the report

From the project directory, render the analysis document:

```bash
quarto render path/to/report.qmd --to html
```

Replace `path/to/report.qmd` with the actual Quarto report path.
Alternatively, open the document in RStudio and click **Render**.

VEP annotation is an external step. Use the documented submission
settings and exported VEP results to reproduce that part of the analysis.

## Reproducibility

The project records:

- Analysis code and interpretation in Quarto.
- R package versions in `renv.lock`.
- Random seeds for stochastic analysis steps.
- VEP submission settings and exported results.
- Software information from `sessionInfo()`.
- Changes to code and documentation through Git.

## Acknowledgments

This project was completed as part of a functional genomics practical.
The data and teaching workflow were supplied with the course materials.

_Supervising instructor_: **Dominic Wright**, Professor, HBIO, Molecular Genetics and Bioinformatics

## Author

**Dakouri Kobri**<br>
Data Science, AI/ML, Bioinformatics, Pharmacology, Toxicology<br>
& Health Science Enthusiast

[LinkedIn](https://www.linkedin.com/in/dakouri-m-kobri-009192208/)

## Resources

- [cTWAS](https://xinhe-lab.github.io/ctwas/)
- [Ensembl Variant Effect Predictor](https://www.ensembl.org/tools/vep/)
- [Quarto](https://quarto.org/)
- [renv](https://rstudio.github.io/renv/)
