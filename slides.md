# Comp Genomics 2016

## Genome Assembly Basics

Members: Wilson Martin, Tannishtha Som,  Alli Gombolay, Tyrone Lee, Peijue Zhang, Ellie Kim, Cheng Chen, Alicia Francis, Namrata Kalsi, Aroon Chande

###### Click [here](/?print-pdf) for a print freindly version

---

## Outline

- Illumina Sequencing 
- Genome Pipeline
  - Quality Control and pre-processing
  - Read assembly: *de novo* and reference guided assembly 
  - Assembly improvement
  - Assembly quality assessment 

---

## Illumina Sequencing
###Sequencing method
- "Sequence by synthesis"
	- Sample DNA is sheered and ligated to primers
	- Bridge amplification 
	- Sequencing reaction
- Each insert has a tag, or barcode
	- The barcode is unique for each DNA sample in run
	- Barcode is read as part of the synthesis reaction

---

## Paired end sequencing

- Reads from both ends of the insert
- Insert is of unknown size
	- Estimated average provided by sequencing facility
- PE help orient reads during assembly
	- Spatial constrainsts for how far about pairs can be placed

---

## Data we have

- Illumina PE, 250bp reads
	- From a HiSeq2500
	- Already demuliplexed

---

##  Genome Pipeline
  - Quality Control and pre-processing
  - Read assembly: *de novo* and reference guided assembly 
	- Types of *de novo* assemblers
	- Assembly programs chosen for testing
  - Assembly improvement
	- Polishing
	- Gap filling
	- Contig integration
	- Automated SNP calling for reference guided assemblies
  - Assembly quality assessment 


---


## Quality Control and pre-processing

- Remove barcodes
- Remove poor quality reads
- Filter duplicates (Typically for speed considerations)

---

## QC software

- Sickle
- Quake
- Musket
- Prinseq
- FastQC
	- Trim Galore!

---

### Read assembly: *de novo* and reference guided assembly

- *De novo*
	- SPAdes, Velvet, whatever else
	- Use only sequence information to order reads 
- Reference Guided
	- bwa/bowtie, SMALT, PILON
	- Reference must be closely related

---

## *De novo* assembly

- Attempts to order reads using their sequence
- Two methods
	- Overlap Layout Consensus
	- de Bruijn graphs

---

## Overlap Layout Consensus

- "Old", computational expensive
- Assembly method:
	1.  Find the two reads with best overlap across the whole read
	2.  Find the next read that overlaps with #1
	3.  Repeat

---

## de Bruijn graphs

- Fast, memory and space efficient
- Resolution of ambiguous read placement
- Assembly method:
	1.  Break reads into mers of size k (smaller than read length)
	2.  Find overlaps of kmers (computationally easier than OLC)
	3.  Resolve ambiguities using estimated genomic distances

---

## Reference guided

- Reconstruct genome of interest using:
	1.  Genome of a closely related organism
	2.  Raw reads of interest mapped for the above genome
- Genome is reconstructed by taking the consensus call for a give base
- Much faster than *de novo*, especially for strains of the same species
- Variant calling using same mapped data


---

## Assembly improvement
- Polishing - Fixing short indels and miscalls
- Gap filling - Remove N's and extending contig ends
- Contig integration - Merging two assemblies
- Automated SNP calling for reference guided assemblies

---

## Polishing and Gap filling

- Polishing - PILON, IMAGE2
	- Map raw reads to check for consistency
	- SPAdes does this automatically using bayeshammer during assembly
- Gap Filling - Sealer (ABySS), PILON, GMcloser, IMAGE2
	- Map raw reads to assembly and use low-coverage information 
	- Doesn't always work, some regions are just not sequenced

---

## Contig integration

- Attempt to build better assemblies by combining multiple assemblies
	- Typically from different asseblers
	- Some assembly algorithms are strict and produce shorter, low error contigs
	- Some are greedy and produce longer contigs with a higher error rate
- Contig integration requires that input assemblies have high homology

---

### Automated SNP Calling during refinement

- Part of PILON's internal pipeline
- Uses the SNP calling pipeline from samtools on alignment 
	generated during polishing and gap closing
- Applies some statistical models to suppress low quality SNP calls

---

## Assembly quality assessment

- Quast
- SuRankCo
- qaTools

---

Thanks
