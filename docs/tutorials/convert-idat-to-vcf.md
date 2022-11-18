---
title: Coverting Illumina IDAT to VCF/PLINK BINARY
layout: pages
---

### Content

1. [Requirements](#requirements)
2. [Step-by-Step procedure](#procedure)

* * *

## Requirements

1. Illumina Array Analysis Platform Genotyping Command Line (iaap-cl)

2. The gtc2vcf bcftools plugin

3. Manifest and cluster files for the chip used to generate your IDAT files
- The manifest for the chip used to generate your data should typically be provided to you
- If you used the **H3Africa chip**, these files can be downloaded from [here](https://chipinfo.h3abionet.org/downloads) 
- You can find more resources from the Illumina website [here](https://emea.support.illumina.com/array/downloads.html)

* * *

## Step-by-step procedure <a name="procedure"></a>

### Download iaap-cli

- This can be downloaded from [here](https://emea.support.illumina.com/downloads/iaap-genotyping-cli.html)

  **Note** You need to create an account, and then you can download it freely.

- Alternatively, you can run the code below (linux). This was adapted from [the gtc2vcf github page](https://github.com/freeseek/gtc2vcf)


***Linux users***
```shell
wget ftp://webdata2:webdata2@ussd-ftp.illumina.com/downloads/software/iaap/iaap-cli-linux-x64-1.1.0.tar.gz
```

***Mac users***
```shell
curl ftp://webdata2:webdata2@ussd-ftp.illumina.com/downloads/software/iaap/iaap-cli-linux-x64-1.1.0.tar.gz --output iaap-cli-linux-x64-1.1.0.tar.gz
```

### Install iaap-cli

The following instructions have been adapted from [the gtc2vcf github page](https://github.com/freeseek/gtc2vcf). 
You may visit the github page for further useful information

***setup some relevant paths***
```shell
mkdir -p $HOME/bin && cd /tmp
```

***Extract and place iaap-cli in the relevant paths***
```shell
tar xzvf iaap-cli-linux-x64-1.1.0.tar.gz -C $HOME/bin/ iaap-cli-linux-x64-1.1.0/iaap-cli --strip-components=1
```

### Get a pre-compiled binary of gtc2vcf plugin for bcftools

***First***, create a new directory for your IDAT to VCF project in a location of your choice and migrate to the direcotry.
```shell
mkdir -p idat2vcf
cd idat2vcf
```

***Note: I always use -p to avoid overwriting a directory if it already exists***

***Next***, check your version of bcftools by typing bcftools

```shell
bcftools
```

***Next***, go to [https://software.broadinstitute.org/software/gtc2vcf/](https://software.broadinstitute.org/software/gtc2vcf/) 
and download a pre-compiled version of gtc2vcf by clicking on `binaries` for the version that corresponds to your version 
of bcftools. 

It will still work if your version of bcftools is higher than the version of gtc2vcf but not the other way round.

<p align="center">
  <img src="/tutorials/gtc2vcf-website.png" alt="https://software.broadinstitute.org/software/gtc2vcf/">
</p>


***Note: Make sure your version of bcftools is greater than or equal to the version of gtc2vcf***

**Example**

*Linux users*
```shell
wget https://software.broadinstitute.org/software/gtc2vcf/gtc2vcf_1.15.1-20220518.zip
```

*Mac users*
```shell
curl https://software.broadinstitute.org/software/gtc2vcf/gtc2vcf_1.15.1-20220518.zip --output gtc2vcf_1.15.1-20220518.zip
```

*Notice that this is version 1.15.1 for bcftools version 1.15.1 or higher*

***Next***, unzip the newly downloaded file
```shell
unzip gtc2vcf_1.15.1-20220518.zip
```

*You should see three files in the current directory*
```shell
ls

# gtc2vcf.so
# affy2vcf.so
# gtc2vcf_plot.R
```

We will use `gtc2vcf.so` to process our Illumina IDAT files

