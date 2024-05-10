# Cancer Research Data Analysis in Python

This document provides an overview of a Python script used for analyzing data related to cancer research, specifically focusing on clinical and somatic mutation data from cancer patients. The script merges data, performs exploratory data analysis (EDA), and identifies significant cancer driver genes through statistical testing.

## Setup and Initialization

The code begins by setting up the environment and loading the necessary files:

- **Current Working Directory**: The script sets the current working directory using `os.getcwd()`.

- **File Paths**: It uses `glob.glob` with recursive search (`recursive=True`) to find clinical and somatic files in the working directory and all its subdirectories. The code sorts the lists of files for further processing.

## Identifying Cancer Types

The script initializes a dictionary (`cancer_pairs`) to hold lists of somatic and clinical file pairs for each cancer type. Then, it processes each file in the list of file paths:

- If the file name contains `'somatic'`, the script extracts the cancer type from the file name and appends a dictionary with the somatic file path to the corresponding list in `cancer_pairs`.

- If the file name contains `'clinical'`, the script extracts the cancer type from the file name and appends a dictionary with the clinical file path to the corresponding list in `cancer_pairs`.

## Merging Somatic and Clinical Data

For each cancer type and its list of pairs in `cancer_pairs`:

- The script initializes `somatic_data` and `clinical_data` to `None`.

- It reads data from somatic and clinical files using `pd.read_csv()`, handling file compression and delimiter issues as needed.

- The script extracts additional data from `somatic_data`, including affected protein and protein length, reference and alternative alleles, and patient identifier.

- It merges somatic and clinical data on the 'patient' column using `pd.merge()`.

## Exploratory Data Analysis (EDA) Functions

The script contains several functions (`clinical_EDA`, `somatic_EDA`, `cancer_driver_genes`) that perform exploratory data analysis (EDA) on clinical and somatic data, as well as identify significant cancer driver genes.

### `clinical_EDA`

This function performs exploratory data analysis on clinical data:

- **Gender Proportions**: Calculates gender proportions and plots the distribution.

- **Age Analysis**: Analyzes age at diagnosis, including range, average, and distributions using box plots and histograms.

- **Age Distribution by Gender**: Compares age distributions between male and female patients.

### `somatic_EDA`

This function performs exploratory data analysis on somatic mutation data:

- **Mutation Analysis**: Analyzes mutation counts, types, and distributions, using bar charts and box plots.

- **Relationship Analysis**: Investigates the relationship between mutation counts and patient data (age, tumor stage).

### `cancer_driver_genes`

This function identifies significant cancer driver genes through statistical testing:

- **Gene Expected Data**: Reads and processes gene expected data.

- **Somatic Data**: Reads and processes somatic data.

- **Statistical Testing**: Calculates observed and expected mutation frequencies, performs chi-square tests, and applies Bonferroni correction for multiple comparisons.

- **Significant Genes**: Identifies and reports significant cancer driver genes based on p-values and chi-square statistics.

## Usage

The functions in the script can be called with appropriate file paths as arguments. The code prints results of the analyses, such as merged data shapes, statistical test results, and significant genes.

By merging clinical and somatic data, performing EDA, and identifying significant cancer driver genes, this script provides valuable insights into cancer-related data and helps advance cancer research.
