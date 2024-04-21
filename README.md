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
>the fastq that has been downloaded will be stored within the current directory.
>
>you can change where it has been stored within the script or later
>
>also, there is a new version called **fasterq-dump**, in the future, it might be better to use this function
>
>Once, there is the raw fastq, I copied them into additional folder within **downloaded_SRA**, called **fastq**, the original will stay there as backup
>
>to copy a file, command line works but if there is a lot, might want to use the **copy** script
