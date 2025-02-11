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

### Running GenFlow ▶️

GenFlow is executed with the following command structure:

```bash
GenFlow -o path/to/working_directory [options]
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

3. The identifier of your sample (must be unique).

Ex: If your input files are : 'ATH10293.R1.fastq' and 'ATH10293.R2.fastq', then it is recommanded to select `ATH10293`or `10293`.

### Important Notes ⚠️📝✅
**Avoid overwriting inputs**: If an incorrect path or name is entered, use `Ctrl + C` to exit and restart the command rather than editing directly.

### Troubleshooting 🛑🔍

- **Invalid option error**: Double-check the command syntax.
- **Missing `SampleSheet.txt`**: The script generates it automatically, but ensure permissions are correct.
- **Pipeline execution failure**: Check that input paths are correct

## 3. VarCheck: Prediction Tools' Annotation 🧬🔍

VarCheck is a complementary tool to GenFlow, designed for assessing the functional impact of detected variants by integrating additional annotation scores.

### Purpose 🎯

VarCheck enriches variant annotations by integrating prediction tools that assess the deleteriousness of variations found in VCF files.

### Running VarCheck ▶️

To run VarCheck on a VCF file:

```bash
VarCheck [-o output_directory] input.vcf
```

This command outputs an annotated VCF file with additional prediction scores.

## License 📜

This software is provided "as is" without any warranties. Use and modify it at your own risk.

## Author ✍️

Developed by Rouquet Pierre, IGBMC

