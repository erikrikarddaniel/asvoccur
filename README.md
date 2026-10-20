# asvoccur
R tools for ASV occurrence data in [SBDI](https://biodiversitydata.se/).

See [Releases](https://github.com/biodiversitydata-se/asvoccur/releases) for the changelog.

## Overview
The **asvoccur** R package, currently under development, provides tools for unpacking and processing ASV occurrence data and metadata downloaded from [the Swedish ASV portal](http://asv-portal.biodiversitydata.se/). It enables users to convert condensed DwC archives into ASV table format for easier downstream analysis in R, by using functions that load, merge, and aggregate ASV counts across taxonomic ranks.

## Tutorial
See our [tutorial](https://biodiversitydata-se.github.io/sbdi-days-eDNA/tutorial.html) for an example workflow using **asvoccur** with ASV portal data in R.

## Install
```R
install.packages('remotes')
remotes::install_github("biodiversitydata-se/asvoccur")
# or:
# remotes::install_github("biodiversitydata-se/asvoccur@develop")
library(asvoccur)
```
GitHub installations (local source builds) may occasionally fail. If so:
```R
remove.packages("asvoccur")
# restart R / RStudio
remotes::install_github("biodiversitydata-se/asvoccur", force = TRUE)
```

## Run
```R
data_path <- '/path-to/dataset-folder'
loaded <- load_data(data_path)
merged <- merge_data(loaded)
summed <- sum_by_clade(merged$counts, merged$asvs)
summed_df <- convert_to_df(summed)
```

### Parquet tables for large datasets
`asv_to_parquet()` converts the downloads to Parquet tables with DuckDB, without reading the data into R.
```R
asv_to_parquet('/path-to/dataset-folder', out_dir = '/path-to/parquet')
# In DuckDB: read_parquet('/path-to/parquet/occurrence/*/*.parquet', hive_partitioning = true)
```
With `name_convert = 'ecolongr'` the keys are named `sample`, `taxon` and `quant`, all other columns are snake_case, and the tables can be passed to [ecolongr](https://github.com/biodiversitydata-se/ecolongr) as they are.

## Get help
```R
?asvoccur::load_data
?asvoccur::asv_to_parquet
?asvoccur::merge_data
?asvoccur::sum_by_clade
?asvoccur::convert_to_df
```
