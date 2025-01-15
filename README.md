## BRF ONT Amplicon
This is a preparation script that readies a multiplexed ONT sample directory tree
for processing by the ONT Epi2me amplicon pipeline: 
https://github.com/epi2me-labs/wf-amplicon

### Download and Setup
This pipeline requires a 64-bit Linux system and python (supported versions are python3.8 and higher).

Download the pipeline via Git:
```bash
git clone brf_ont_amplicon
```

External dependencies:
* minimap2
* samtools
* Nanofilt (deprecated and to be replaced with Chopper - requires Ubuntu 20 or later)
* Nextflow
* Singularity - make sure you have temporary directories assigned as environment variables
  for temp files and working space

Each of these by default will be expected to be found in $path, but full paths for each 
can be provided as command line arguments to plasmid_prep.py

### Running the prep
Call amp_prep.py with command line arguments for the existing ONT data source, 
the output directory, and any other parameters as required. This will produce a new
directory tree that is populated with the files and structure expected by the ONT
wf-amplicon pipeline. It is possible to enable pre-assembly filtering of reads
by adjusting the run scripts that are produced for each client.

### Output:
- amp_dir/
  - clientA/
    - fastq1...fastqN (.gz possible)
  - clientB/
    - ...
  - ...

### Running the amplicon processing
To perform the actual pipeline, ensure that the whole output directory tree is available 
to the machine that will run the pipeline. Then you can simply execute the bash script
"run_amplicons.sh" in the top-level directory. This will execute each client pipeline sequentially.

