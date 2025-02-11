# GenFlow - NGS Analysis Pipeline

## Summary 🚀🧬📊

GenFlow is a comprehensive tool designed for Next-Generation Sequencing (NGS) analysis, specifically handling Whole Exome Sequencing (WES) and Whole Genome Sequencing (WGS) data. The pipeline automates variant calling and primary annotations. Additionally, it integrates secondary tools for further annotation and impact assessment of variants.

## 1. Setup & Installation ⚙️🛠️📥

Before using GenFlow, the module must be set up correctly. This step is required only once.

### Initial Configuration 🔧📑💻

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

### Running GenFlow ▶️📜📈

GenFlow is executed with the following command structure:

```bash
GenFlow [command] [options]
```

This command initiates the variant calling pipeline, processing raw sequencing data to generate a list of variants with primary annotations.

### Important Notes ⚠️📝✅

1. Ensure that the sample name does not appear multiple times within the data directory.
2. If your data directory is located inside your working directory (e.g., `NGS_analysis/data`), use `data` as the relative path; otherwise, provide the absolute path.
3. **Avoid overwriting inputs**: If an incorrect path or name is entered, use `Ctrl + C` to exit and restart the command rather than editing directly.

### Troubleshooting 🛑🔍🛠️

- **Invalid option error**: Double-check the command syntax.
- **Missing `SampleSheet.txt`**: The script generates it automatically, but ensure permissions are correct.
- **Pipeline execution failure**: Verify dependencies and correct path settings.

## 3. VarCheck: Prediction Tools' Annotation 📊🧬🔍

VarCheck is a complementary tool to GenFlow, designed for assessing the functional impact of detected variants by integrating additional annotation scores.

### Purpose 🎯🧠📈

VarCheck enriches variant annotations by integrating prediction tools that assess the deleteriousness of variations found in VCF files.

### Running VarCheck 🏃💾📜

To run VarCheck on a VCF file:

```bash
VarCheck [-o output_directory] input.vcf
```

This command outputs an annotated VCF file with additional prediction scores.

## License 📜⚖️🔓

This software is provided "as is" without any warranties. Use and modify it at your own risk.

## Author ✍️🏛️🧑‍🔬

Developed by [Your Name / Lab / Organization]

