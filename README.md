# GenFlow - NGS Analysis Pipeline

## Summary 🚀📊

GenFlow is a comprehensive tool designed for Next-Generation Sequencing (NGS) analysis, specifically handling Whole Exome Sequencing (WES) and Whole Genome Sequencing (WGS) data. The pipeline automates variant calling and primary annotations. Additionally, it integrates secondary tools for further annotation and impact assessment of variants.

## 1. Setup & Installation ⚙️🛠️

### For IGBMC user 📑
Certain prerequisites are necessary if you have never performed scientific calculations on IGBMC platforms.
Here are some interesting notices developed by the IT department to help you understand how it works: 
1. Scientific computing
https://it.igbmc.fr/hpc
2. Quick Start Guide
https://it.igbmc.fr/hpc/quick-start-guide
3. Logging in 
https://it.igbmc.fr/hpc/logging-in
4. SLURM user guide
https://it.igbmc.fr/hpc/slurm-user-guide



### Initial Configuration 📑💻

Before using GenFlow, the module must be set up correctly. This step is required only once.

To make GenFlow available as a module (similar to `bcftools` or `gatk`), add the module path to your environment by running:

```bash
echo 'export MODULEPATH=/shared/space2/laporte/labo6_laporte1/_NGS/GenFlow/modulefiles:$MODULEPATH' >> ~/.bashrc
```

After adding this line, reload your session by disconnecting (`exit`) and reconnecting to ensure the path is recognized.

## 2. GenFlow: Variant Calling and Primary Annotations 🧪🔬📊

GenFlow serves as the primary analysis tool for WES/WGS data, automating variant calling and annotation.

### Loading the Module 📂💻⚡

To use GenFlow, first load the module:

```bash
module load GenFlow
```

### Go in your analysis directory ​🏃‍♂️‍➡️​​📁​

In your personnal folder (in space2 or mendel), it is recommanded to have a main directory where you perform all the analysis of your project.
First get in this directory with `cd path/to/all/analysis`.
Then you are ready to run GenFlow's pipeline.


### Running GenFlow ▶️

GenFlow is executed with the following command structure:

```bash
GenFlow [options] -o outputdir
```

This command runs the full pipeline based on the selected options. The available options are:

- `-g` : Runs the pipeline in Whole Genome Sequencing (WGS) mode.
- `-e` : Runs the pipeline in Whole Exome Sequencing (WES) mode.
- `-c` : Enables Cohort Mode for analyzing multiple samples together.
- `-s` : Runs in Single Analysis Mode for individual sample analysis.
- `-l` : Activates Germline Mode for inherited variant detection.
- `-o [dir]` : Specifies the working directory (mandatory argument).
- `-h` : Displays help information about the available options.

### Sample Sheet Creation ✍️📝

The pipeline include a SampleSheet creation tool to prepare your analysis. There are few informations you need to know before this step : 
1. The location of your raw data (input) :

Ex : `path/to/raw/data`.

⚠️ If your data directory is located inside your working directory (e.g., `NGS_analysis/data`), use `data` as the relative path; otherwise, provide the absolute path.

2. The identifier of your sample (must be unique).

Ex: If your input files are : 'ATH10293.R1.fastq' and 'ATH10293.R2.fastq', then it is recommanded to select `ATH10293`or `10293`.

### Important Notes ⚠️📝✅
**Avoid overwriting inputs**: If an incorrect path or name is entered, use `Ctrl + C` to exit and restart the command rather than editing directly.

### Troubleshooting 🛑🔍

- **Invalid option error**: Double-check the command syntax.
- **Missing `SampleSheet.txt`**: The script generates it automatically, but ensure permissions are correct.
- **Pipeline execution failure**: Check that input paths are correct

### Results and SLURM issues/output 📝✅

- **Results** : Your analysis process will go through 7 steps from raw data to annotation : the resulting .vcf file is in the `/07-annotation` folder. Do not hesitate to check the stat file in the same folder, you will get information about the total number of variant, the number of variants per categories ...
- **Errors** : Errors may happen, you can find additional information about them in the `/slurm_output`folder.

## 3. VarCheck: Prediction Tools' Annotation 🧬🔍

VarCheck is a complementary tool to GenFlow, designed for assessing the functional impact of detected variants by integrating additional annotation scores.
This is a highly recommanded step, but not mandatory. This process will last approximately 1h per 5 000 000 variants. If you don't need it, go directly to step 4.

### Purpose 🎯

VarCheck enriches variant annotations by integrating prediction tools that assess the deleteriousness of variations found in VCF files.

### Running VarCheck ▶️

To run VarCheck on a VCF file:

```bash
VarCheck [-o output_directory] input.vcf
```

This command outputs an annotated VCF file with additional prediction scores.

## 4. VCFilter: Filtering and Transformation of VCF Files 🛠️📈

VCFilter is a tool to filter, transform, and convert VCF files into TSV and Excel formats for easier downstream analysis.
Now that you have done your analysis with GenFlow (and eventually VarCheck), you can proceed to the extraction of the variants in order to get an Excel file.
If your .vcf file is huge (more than 100 000 Kb), it is recommanded to filter your results. 
Your can wether filter on the impact of the variant or the frequency on gnomAD (healthy population).

Here you have the list of different consequences and the corresponding IMPACT 


![image](https://github.com/user-attachments/assets/999597e9-0e5c-4e2f-ae76-78aa331dd025)
![image](https://github.com/user-attachments/assets/caae0310-6654-45e7-921e-4d3e3911ed31)

### Running VCFilter ▶️

VCFilter can be executed using the following command structure:

```bash
VCFilter [-o output_directory] [-f gnomADfrequency] [-i IMPACT] input.vcf|input.tsv
```


Available options:

- `-o (directory)`: Output directory (defaults to input file's directory if not specified).
- `-f (number)`: Filters variants by gnomAD frequency (e.g., 0.01 to exclude variants with frequency >1%).
- `-i (IMPACT)`: Filters variants by impact (HIGH, MODERATE, LOW).
- `-h`: Displays help information.

### Example Usage:

```bash
VCFilter -o results_folder -f 0.01 -i HIGH sample.vcf
```

### Output:

- A filtered `.tsv` file containing selected variants.
- A sorted `.csv` file ready for further analysis.
- (Optional) An Excel `.xlsx` file for easier visualization.

To convert the final CSV file to Excel, you will be prompted to confirm:

```bash
Do you want to convert to Excel? This might take some time (y/n):
```

## 5. VarRadar: Quantile-Based Annotation and Radar Plot Generation 📊📡

Finally that you have your Excel, you may find interesting missense variants. VarRadar is a visualization tool designed to analyze annotation scores based on quantiles and generate a radar plot for a given variant. This allows for an intuitive comparison of a variant’s impact across different annotation metrics.

<img src="https://github.com/user-attachments/assets/d40e042f-a0cb-4bc8-9971-123637a0db13" width="400">


### Purpose 🎯
VarRadar provides a graphical representation of annotation scores, helping to compare the relative significance of variants based on their functional impact.

### Running VarRadar ▶️
To run VarRadar, use the following command structure:

```bash

VarRadar [-c chromosome] [-p position] input.csv
````

Available options:

`-c (chromosome)`: Chromosome identifier (e.g., chr1).
`-p (position)` : Variant position (e.g., 103293).
`-h ` : Displays help information.

Example Usage:
```bash

VarRadar -c 1 -p 103293 sample.csv

```

## Input Requirements 📝

The input file must be in CSV format (`.csv`).
The chromosome and position of the variant must be specified.

## Output 📈

A radar plot visualizing the annotation scores.
A log message confirming successful execution or detailing errors.
Troubleshooting 🛑🔍
`Missing input file`: Ensure a valid CSV file is provided.
`Incorrect format`: The tool only accepts .csv files.
`Execution failure`: Check that chromosome and position arguments are correctly formatted.


## License 📜

This software is provided "as is" without any warranties. Use and modify it at your own risk.

## Author ✍️

Developed by Rouquet Pierre, IGBMC
