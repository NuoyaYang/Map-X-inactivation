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
>original: **SRR8427168_1.fastq.gz**  the correct version:**SRR8427168_S1_L001_R1_001.fastq.gz**;
>
>hence, the sample within the **alignment** will be **SRR8427168**.

**Run cellSNP-lite**
>In order to run cellSNP-lite, you need a few files: #BAM, #barcodes, #reference SNP
>
>But before you run your own data, please download the **cellSNP_testdata_10x** folder from this following link:
>
>https://sourceforge.net/projects/cellsnp/files/SNPlist/
>
>I then logout HPC
```
cd /Users/laurayang/Download
scp -r ./cellSNP_testdata_10x nuoyayan@discovery.usc.edu:/project/swang585_1200/cellSNP
```
>then computer will have the following pop up
```
nuoyayan@discovery.usc.edu's password:
```
>type in your discovery login password and then the file will be copied from your local computer onto HPC and then you can log into hpc to check it. Make sure the file is there and you can now do a test run with the file provided. You can run it in interactive node or using the script **cellSNP**.
>
>Once you passed the test run, again use the script **copy** to get your processed #BAM, #barcodes, and #reference SNP **hg38** from either the **cellranger count** or
```
>wget http://ufpr.dl.sourceforge.net/project/cellsnp/SNPlist/genome1K.phase3.SNP_AF5e2.chr1toX.hg38.vcf.gz
```
>from this link: https://sourceforge.net/projects/cellsnp/files/SNPlist/.
>Then, you can run cellSNP-lite pipeline following instructions from this link: https://cellsnp-lite.readthedocs.io/en/latest/main/manual.html. I used the **1a mode**.



scp nuoyayan@discovery.usc.edu:/project/swang585_1200/ANNOVAR/annovar/myanno.hg19_multianno.csv /Users/laurayang/Desktop
