# [Snakemake](johanneskoester)

## Scalable bioinformatics workflow engine
## Developer: Johannes Koster

---

# GNU Make

## the good
- text based
- rule pardigm
- lightweight
- initial release 1977

## the bad and ugly
- cryptic syntax
- limited scripting
- missing support for multiple output files and wildcards
- no cluster support

---

# Rules

```yaml
rule myrule:
	input : ”path/to/{sample}. txt”
	output : ”path/to/{sample}.column1. txt”
	shell : ”cut - f1 < {input} > {output}”
```

## Example

```yaml
SAMPLES = ”500 501 502 503”. split ()

# define subworkflow
subworkflow mapping:
	workdir: ”../mapping”
	
rule all:
	input :
		expand(”{sample}/results.xprs”, sample=SAMPLES)
		# estimate transcript expressions
rule express:
	input:
		REF,
		mapping(”{sample}.bam”)
	output:
		”{sample}/results . xprs”
	shell:
		”express {input} -o {wildcards.sample}”
```
# more features

```bash
# visaulize the DAG of jobs
snakemake --dag | dot | display

# dry-run
snakemake -n

# execute using 8 cores
snakemake --cores 8

# execute on the cluseter
snakemake --jobs 20 --cluster "qsub -pe threaded {threads}"

# execute on the cluseter using DRMAA API
snakemake --jobs 20 --drmaa
```

# Summary
- a readable syntax
- scripting with Python
- scalability form single-core to cluster and hybrid computing
- data provenance
- modularization