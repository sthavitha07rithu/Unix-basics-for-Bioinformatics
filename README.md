# STCC Mini Project: Unix Basics for Bioinformatics

## Overview

This repository documents Unix and Git command-line concepts learned during the STCC course, with an emphasis on their application in bioinformatics and genomic data analysis workflows. The material covers Unix file system navigation, text processing, command chaining, data inspection, and version control using Git and GitHub.

The README is written as a clear guide that can be reused and understood by others, rather than just a list of commands, and follows good bioinformatics documentation practices.

---

## Learning Objectives

By completing this mini project, I demonstrate the ability to:

* Navigate Unix/Linux file systems confidently
* Manipulate and inspect biological data files using standard Unix utilities
* Chain commands using pipes and redirection
* Understand common bioinformatics file formats (FASTA, GTF, BED, tabular text)
* Use Git and GitHub for version control and collaborative research

---

## Data Availability

Small example FASTA and TXT files used to demonstrate Unix commands are provided in the directory.
Large reference files (e.g., Mus_musculus.GRCm38.75.gtf) are intentionally not stored in this repository and should be downloaded from official sources.


## 1. Unix File System Navigation

```bash
pwd        # Show current working directory
ls         # List files and directories
ls -l      # Detailed listing
cd data/   # Change directory
cd ..      # Move one directory up
```

**Key points**

* Unix is case-sensitive.
* Absolute paths start from `/`, while relative paths depend on the current directory.

---

## 2. Creating and Managing Files and Directories

### Creating files and directories

```bash
mkdir test-project
touch random.csv
```

### Writing to and viewing files

```bash
echo "Hello World" > random.csv
echo "Hello India" >> random.csv
cat random.csv
```

### Copying, moving, and renaming

```bash
cp demo_1/random.csv -t demo_2
mv demo_1/random.csv demo_2
mv demo_2 test
```

### Deleting files and directories

```bash
rmdir empty_dir
rm file.txt
rm -rf test
```

**Note:** File deletion in Unix is permanent; there is no recycle bin.

---

## 3. Getting Help and Tracking Commands

```bash
man ls        # Command manual
history       # List previously executed commands
```

Manual pages are essential for understanding command options and correct usage.

---

## 4. Pattern Matching and File Subsetting

### Brace expansion

```bash
echo languages-{python,r,rust}
touch sample{A,B,C}_R{1,2}.fastq
```

### Wildcards and ranges

```bash
ls sampleA*
ls sample[AB]_R1.fastq
ls sample[A-C]_R1.fastq
```

These patterns are commonly used when handling multiple sequencing files.

---

## 5. Streaming, Redirection, and Pipes

### Streaming large files

Streaming allows inspection of large biological files without loading them entirely into memory.

```bash
cat tb1_protein.fasta tb1.fasta
```

### Output redirection

```bash
cat tb1_protein.fasta tb1.fasta > combined.fasta
cat tga1-protein.fasta abc.fasta > combined.fasta 2> combined.stderr
```

### Pipes

A pipe (`|`) sends the output of one command as input to the next.

```bash
grep -v "^>" tga1-protein.fasta | grep --color "[^GPSTVEF]"
```

This example removes FASTA headers and highlights unexpected amino acids in protein sequences.

---

## 6. Inspecting and Querying GTF Annotation Files

### Viewing large annotation files

```bash
cat Mus_musculus.GRCm38.75.gtf | less
```

### Inspecting file content

```bash
head Mus_musculus.GRCm38.75.gtf
head -n 20 Mus_musculus.GRCm38.75.gtf
tail Mus_musculus.GRCm38.75.gtf
```

### Searching for specific gene IDs

```bash
grep 'gene_id "ENSMUSG00000095742"' Mus_musculus.GRCm38.75.gtf
grep -o 'gene_id "ENSMUSG00000095742"' Mus_musculus.GRCm38.75.gtf
```

### Counting occurrences

```bash
grep 'gene_id "ENSMUSG00000095742"' Mus_musculus.GRCm38.75.gtf | wc
```

Selective counts:

```bash
wc -l   # lines
wc -w   # words
wc -m   # characters
```

---

## 7. Version Control with Git and GitHub

### Git configuration and SSH setup

```bash
git config --global user.name "your-username"
git config --global user.email "your-email"
ssh-keygen -t rsa -b 4096 -C "your-email"
```

The public SSH key (`id_rsa.pub`) is added to the GitHub account for secure authentication.

### Basic Git workflow

```bash
git init
git add filename
git commit -m "commit message"
git status
git diff
git log
```

### Undoing changes

```bash
git restore filename
git restore --staged filename
git rm -f filename
git mv oldname newname
```

### Ignoring files

```bash
touch .gitignore
echo "sample.fastq" >> .gitignore
git add .gitignore
git commit -m "Add gitignore"
```

### Pushing to and pulling from GitHub

```bash
git remote add origin <repository-url>
git branch -M master
git push origin master
git pull origin master
```

---

## 8. Working with Tabular and Genomic File Formats

### BED files

```bash
head chr20_100kb_windows.bed
tail chr20_100kb_windows.bed
head -n 5 chr20_100kb_windows.bed
(head -n 3 < chr20_100kb_windows.bed; tail -n 3 < chr20_100kb_windows.bed)
```

### Cutting and formatting columns

```bash
cut -f 2 chr20_100kb_windows.bed | head -n 3
grep -v "^#" Mus_musculus.GRCm38.75.gtf | cut -f1,4,5 | head -n 3
```

Aligning output for readability:

```bash
grep -v "^#" Mus_musculus.GRCm38.75.gtf | cut -f1-8 | head -n 3 | column -t
```

### Grep pattern matching

```bash
grep "MLPH" genes.txt
grep ENSG000001 genes.txt
grep ENSG000001 genes.txt | grep -v "ENSG00000173467"
```

Context options:

```bash
grep -B1 "TACTTG" SRR15006374_1.fastq
grep -A2 "TACTTG" SRR15006374_1.fastq
```

Regular expressions:

```bash
grep "FOX[AC]" genes.txt
grep -E "(FOXC|FOXA)" genes.txt
grep -c "FOXC" genes.txt
```

---

## 9. Sorting, Uniqueness, and Pipelines

```bash
sort letters.txt | uniq
sort letters.txt | uniq -c
```

Sorting by columns:

```bash
sort -k1,1 file.txt
sort -k2,2 file.txt
sort -k2,2n file.txt
```

Pipeline example:

```bash
grep -v "^#" Mus_musculus.GRCm38.75_chrl.gtf | cut -f3 | sort | uniq -c
```

---

## 10. Joining Files

```bash
sort -k1,1 example.bed > example_sorted.bed
join -1 1 -2 1 example_sorted.bed example_lengths.txt > example_join.bed
```

This operation joins genomic intervals with chromosome length information using a shared key.

---

## 11. Reproducible and Robust Research Practices

### Reproducible research

* Share code and data
* Record software and data versions
* Maintain metadata
* Document workflows clearly

### Robust research

* Write readable, modular code
* Automate repetitive tasks
* Use consistent naming conventions
* Treat raw data as read-only
* Use README files as project manuals

---

## Conclusion

This repository serves as a structured record of Unix, Git, and bioinformatics command-line concepts learned during the STCC course. The documented practices form the foundation for reproducible, scalable, and robust computational biology workflows.
