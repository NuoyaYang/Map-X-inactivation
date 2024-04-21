# Map-X-inactivation

**Implement cellSNP-lite pipeline**(_the latest version, the older version is called cellSNP_)
>login to the CARC cluster over ssh
```
ssh nuoyayan@discovery.usc.edu
```
>password is same as usc email
```
cd /project/swang585_1200
module purge
module load conda
conda init bash
source ~/.bashrc
```
>only have to create the environment once, mamba or conda both works, switch command when do so
```
conda create -n cellsnp
conda activate cellsnp
conda install -c bioconda cellsnp-lite
conda deactivate
```
**Download SRA to test the pipeline**
```
cd /project/swang585_1200
ls
```
>should have three files: **ANNOVAR**, **cellSNP** & **downloaded_SRA**
>
>within downloaded_SRA: there is a script named **SRAdownload** that download SRA file with accession number and then turn it into fastq
```
sbatch download
```
>The fastq files that have been downloaded will be stored within whatever directory you wrote your script in,but you can change where it will be stored within the script or later.
>
>Also, there is a new version called **fasterq-dump**, it might be better to use this function in the future.
>
>Once there is the raw fastq, I copied them into a new folder within **downloaded_SRA**, called **fastq**, the original will stay in **downloaded_SRA** as backup.
>
>To copy a file, command line works but if there is a lot data, one might want to use the **copy** script.
>
**Align fastq Reads**
>To align 10x genomic scRNA-seq reads, the recommanded software is **cellranger count**.
>
>Here is the website tutorial that will be helpful:
>
>https://www.10xgenomics.com/support/software/cell-ranger/latest/tutorials/cr-tutorial-ct
>
>I wrote a script named **alignment** that will run it, but please adjust it accordingly.
>
>before you run the cellranger count, you have to change all the fastq file name into a specific format like such:
>
>original: **SRR8427168_1.fastq.gz**  the correct version:**SRR8427168_S1_L001_R1_001.fastq.gz**; hence, the sample name within the **alignment** will be **SRR8427168**.
