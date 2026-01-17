# Unix-basics-for-Bioinformatics
This repository documents Unix command-line concepts and tools learned during the STCC course. It focuses on file system navigation, command chaining, and practical use-cases relevant to bioinformatics workflows.

# STCC Mini Project: Unix Basics for Bioinformatics

## Overview

This repository documents Unix command-line concepts and tools learned during the STCC course. The focus is on file system navigation, command execution, command chaining, and practical use-cases relevant to bioinformatics and genomic data analysis workflows.

The material is organized by conceptual topics rather than lecture order, to emphasize understanding, reproducibility, and real-world applicability.

---

## Learning Objectives

By completing and documenting this project, I demonstrate the ability to:

* Navigate Unix file systems confidently
* Execute and combine Unix commands for data inspection and manipulation
* Understand how Unix tools integrate into bioinformatics pipelines
* Use GitHub as a professional documentation and learning space

---

## 1. Unix File System Navigation

### Key Commands

```bash
pwd        # Show the present working directory
ls         # List files and directories
ls -l      # List files with detailed information
cd data/   # Change directory
cd ..      # Move one level up in the directory hierarchy
```

### Notes

* Unix is **case-sensitive**.
* Absolute paths start from the root directory `/`.
* Relative paths depend on the current working directory.

---

## 2. Creating and Managing Files and Directories

### Directory and File Creation

```bash
mkdir test-project      # Create a new directory
touch random.csv        # Create an empty file
```

### Writing and Viewing File Contents

```bash
echo "Hello World" > random.csv    # Write text (overwrite)
echo "Hello India" >> random.csv   # Append text
cat random.csv                      # Display file contents
```

### Copying, Moving, and Renaming

```bash
cp demo_1/random.csv -t demo_2   # Copy file to target directory
mv demo_1/random.csv demo_2      # Move file
mv demo_2 test                   # Rename directory
```

### Deleting Files and Directories

```bash
rmdir empty_dir     # Delete empty directory
rm file.txt         # Delete a file
rm -rf test         # Force delete directory with contents
```

**Important:** Unix deletions are permanent. There is no recycle bin.

---

## 3. Getting Help and Command History

```bash
man ls        # Open the manual page for a command
history       # List commands used in the current session
```

Manual pages are essential for understanding command options and correct usage.

---

## 4. Pattern Matching and File Subsetting

### Brace Expansion

```bash
echo languages-{python,r,rust}
touch sample{A,B,C}_R{1,2}.fastq
```

### Wildcards and Ranges

```bash
ls sampleA*
ls sample[AB]_R1.fastq
ls sample[A-C]_R1.fastq
```

These patterns are especially useful when working with multiple sequencing files.

---

## 5. Streaming and Redirection

### Streaming

In Unix-like systems, a *stream* is a flow of data from a source to a destination. Streaming allows inspection of large biological files without loading them entirely into memory.

```bash
cat tb1_protein.fasta
tb1.fasta
```

### Output Redirection

```bash
cat tb1_protein.fasta tb1.fasta > combined.fasta
cat tga1-protein.fasta abc.fasta > combined.fasta 2> combined.stderr
```

Redirection operators:

* `>` overwrite output
* `>>` append output
* `2>` redirect error messages

---

## 6. Pipes and Command Chaining

A pipe (`|`) sends the output of one command directly as input to the next.

```bash
grep -v "^>" tga1-protein.fasta | grep --color "[^GPSTVEF]"
```

### Bioinformatics Context

* Removes FASTA headers
* Highlights unexpected amino acids in protein sequences
* Demonstrates modular, readable command chaining

---

## 7. Inspecting Annotation Files (GTF)

### Viewing Large Files

```bash
cat Mus_musculus.GRCm38.75.gtf | less
```

### Inspecting File Content

```bash
head Mus_musculus.GRCm38.75.gtf
head -n 20 Mus_musculus.GRCm38.75.gtf
tail Mus_musculus.GRCm38.75.gtf
```

### Searching for Specific Features

```bash
grep 'gene_id "ENSMUSG00000095742"' Mus_musculus.GRCm38.75.gtf
grep -o 'gene_id "ENSMUSG00000095742"' Mus_musculus.GRCm38.75.gtf
```

---

## 8. Counting and Summarizing Data

```bash
grep 'gene_id "ENSMUSG00000095742"' Mus_musculus.GRCm38.75.gtf | wc
```

Selective counts:

```bash
wc -l   # number of lines
wc -w   # number of words
wc -m   # number of characters
```

These commands are commonly used to quantify features, reads, or records in genomic files.

---

## 9. Reproducible and Robust Research Practices

### Reproducible Research

* Share code and data
* Record software and data versions
* Maintain metadata
* Document workflows clearly

### Robust Research

* Write readable, modular code
* Use consistent naming conventions
* Automate repetitive tasks
* Treat raw data as read-only
* Use README files as project manuals

---

## Conclusion

Unix command-line tools form the backbone of modern bioinformatics workflows. This repository serves as a documented reference for foundational Unix concepts and demonstrates how they support reproducible and robust genomic data analysis.
