# Preprocess-ATAC-seq

## Use sra-toolkit to get fastq file
* Download: https://github.com/ncbi/sra-tools/wiki/02.-Installing-SRA-Toolkit
* Use `prefetch` and `fasterq-dump` to extract FASTQ-files: https://github.com/ncbi/sra-tools/wiki/08.-prefetch-and-fasterq-dump
* Useful info: https://erilu.github.io/python-fastq-downloader/

## Use Encode pipeline [Hyak]
* Creat a new conda environment for pipeline
  ```
  conda create --name pipeline python=3.9
  conda activate pipeline
  conda install -c "conda-forge/label/cf202003" openjdk
  pip install caper
  pip install croo
  java -version   # should be >= 11
  ```
* Initialize Caper
  ```
  caper init local
  vi ~/.caper/default.conf    # choose a directory to store pipeline output
  ```
* Git clone pipeline GitHub repo: v2.2.2 https://github.com/ENCODE-DCC/atac-seq-pipeline
  ```
  git clone https://github.com/ENCODE-DCC/atac-seq-pipeline
  cd atac-seq-pipeline
  ```
* Run pipeline command on TEST_INPUT_JSON
  ```
  singularity exec docker://ubuntu:latest echo hello      # check if singularity works
  INPUT_JSON="https://storage.googleapis.com/encode-pipeline-test-samples/encode-atac-seq-pipeline/ENCSR356KRQ_subsampled.json"
  caper run atac.wdl -i "${INPUT_JSON}" --singularity --max-concurrent-tasks 1
  ```
* Check output
  ```
  croo YOUR_OUTPUT_PATH/atac/SOME_JOB_ID/metadata.json    # a html file will be generated, download that to local
  ```
