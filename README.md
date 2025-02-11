# GenFlow - NGS Analysis Pipeline

## Summary
GenFlow is the primary tool developed for Next-Generation Sequencing (NGS) analysis, providing workflows for Whole Exome Sequencing (WES) and Whole Genome Sequencing (WGS). After obtaining the list of variants, additional secondary tools have been integrated to further analyze and annotate these variants:

- [GenFlow](#genflow) - The main tool for WES/WGS analysis, including variant calling and annotation.
- [VarCheck](#varcheck) - A secondary tool designed to add annotation scores on deleteriousness of variations in VCF files.
- [Usage](#usage)
- [Important Notes](#important-notes)
- [Troubleshooting](#troubleshooting)
- [License](#license)
- [Author](#author)

## Overview
<details>
<summary>Click to expand</summary>
GenFlow is a tool for whole exome/genome sequencing analysis, including variant calling and annotation. It allows users to process Whole Genome Sequencing (WGS) and Whole Exome Sequencing (WES) data using different analysis modes. The script automates the pipeline execution by setting up the required environment and running the appropriate workflows based on user-defined options.
</details>

## 1st Use (To do only once)
<details>
<summary>Click to expand</summary>
You can load GenFlow as a module (such as bcftools, gatk, etc.). To do so, run the following command in your terminal:

```bash
echo 'export MODULEPATH=/shared/space2/laporte/labo6_laporte1/_NGS/GenFlow/modulefiles:$MODULEPATH' >> ~/.bashrc
```

This will manually add the path of the GenFlow module to the list of available modules. Then, reload your HPC session by disconnecting (`exit`) and reconnecting to ensure that the path has been added.
</details>

## Usual Use
<details>
<summary>Click to expand</summary>
### Loading the Module
When you are in your working directory and want to use the GenFlow tool, load the module:

```bash
module load GenFlow
```
</details>

## Running the GenFlow Command
<details>
<summary>Click to expand</summary>
### Usage
```bash
GenFlow [command] [options]
```
</details>

## Secondary Tools
### VarCheck
<details>
<summary>Click to expand</summary>
VarCheck is a secondary tool designed to add annotation scores on deleteriousness of variations in VCF files.

#### Usage
```bash
VarCheck [-o output_directory] input.vcf
```
</details>

## Important Notes
<details>
<summary>Click to expand</summary>
1. The name of your sample should not appear twice in your data directory.
2. If your data directory is inside your working directory (e.g., `NGS_analysis/data`), just type: `data`.
   Otherwise, use the absolute path: `/shared/space2/laporte/NGS_archive/Athlome/Genomes/1_fastq`.
3. **Avoid overwriting inputs**: If you make a mistake when typing a path or a name, do not erase and retype. This may cause issues with the program. Instead, press `Ctrl + C` to exit and rerun the command:
</details>

## Troubleshooting
<details>
<summary>Click to expand</summary>
- **Invalid option error**: Ensure you are using the correct options as listed above.
- **Missing `SampleSheet.txt`**: The script attempts to create it automatically, but if it fails, check permissions and rerun.
- **Pipeline execution failure**: Check if all dependencies are installed and paths to scripts are correctly set.
</details>

## License
<details>
<summary>Click to expand</summary>
This script is provided "as is" without any warranties. Modify and use it at your own risk.
</details>

## Author
<details>
<summary>Click to expand</summary>
Developed by [Your Name / Lab / Organization]
</details>

