# FTOL

Code repository to generate an automatically updated **Fern Tree of Life**.

Please see the accompanying paper: Nitta JH, Schuettpelz E, Ramírez-Barahona S, Iwasaki W. An open and continuously updated fern tree of life (FTOL)

All code is in **R**, and workflow is controlled with the [targets](https://github.com/ropensci/targets) package.

## Docker

A [docker image](https://hub.docker.com/r/joelnitta/ftol) is available to run the code.

## Setup

Run the [setup.R](R/setup.R) script to create the folder structure needed to store external files and download most of the data files automatically.

```
source("R/setup.R")
```

You should see a new folder called `_targets` appear in the project root. The data files are in `_targets/user/data_raw`.

Alternatively, you can manually create the following folder hierarchy yourself:

```
_targets
└── user
    ├── data_raw
    │   └── ref_aln
    ├── intermediates
    │   ├── blast_sanger
    │   ├── iqtree
    │   │   ├── plastome
    │   │   ├── sanger
    │   │   ├── sanger_1
    │   │   ├── sanger_10
    │   │   ├── sanger_2
    │   │   ├── sanger_3
    │   │   ├── sanger_4
    │   │   ├── sanger_5
    │   │   ├── sanger_6
    │   │   ├── sanger_7
    │   │   ├── sanger_8
    │   │   ├── sanger_9
    │   │   └── sanger_fast
    │   └── treepl
    │       ├── con
    │       ├── ml
    │       └── ts
    └── results
        └── ftolr
```

## Data

### FTOL input data on Figshare

If `setup.R` was run successfully, it will have already downloaded and unzipped the needed files from FigShare.

Alternatively, you can do so manually following these instructions:

Download all of the files contained in the [FTOL input data on FigShare](https://doi.org/10.6084/m9.figshare.19474316.v1) by clicking on the "Download All" button.

Unzip the files and place them in the `_targets/user/data_raw` folder. You will also need to unzip the `ref_aln.tar.gz` archive that is contained within the zip folder.

### Other data files

The following additional data files need to be downloaded and placed in `_targets/user/data_raw`:

- Supplemental Data 1 (1-s2.0-S1055790316302287-mmc2.xlsx) from [Testo and Sundue (2016) Mol. Phylogenetics Evol.](https://doi.org/10.1016/j.ympev.2016.09.003)
- NCBI taxonomy database dump 2022-02-01 (taxdmp_2022-02-01.zip) can be downloaded from the [NCBI FTP server](https://ftp.ncbi.nih.gov/pub/taxonomy/taxdump_archive/taxdmp_2022-02-01.zip).
- [ferncal](https://github.com/fernphy/ferncal) fern fossils database v1.0.0 (fern_fossils.csv) can be downloaded from [here](https://github.com/fernphy/ferncal/archive/refs/tags/v1.0.0.zip).
## Running the code

There are actually two `targets` plans:

- [prep_ref_seqs_plan.R](prep_ref_seqs_plan.R) generates a set of reference FASTA files for extracting target gene regions. These have been made available in the [FigShare data](https://doi.org/10.6084/m9.figshare.19474316.v1), so this generally shouldn't need to be run. But if you want to, it can be run with `tar_make(script = "prep_ref_seqs_plan.R", store = "prep_ref_seqs_store")`.

- [_targets.R](_targets.R) is the main workflow to generate FTOL. This can be run with `targets::tar_make()`.

Note that this code was designed to be run on a multi-core machine, so the number of cores specified (e.g., [here](https://github.com/fernphy/ftol/blob/1c7569eb3bbd93864016bbc1b1df1d11f8d4d62c/_targets.R#L459)) may need to be changed.

The complete workflow takes 1-2 weeks to complete, with phylogenetic analysis taking up by far most of the time.

## License

- code: [MIT](LICENSE)
