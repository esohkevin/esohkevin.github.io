---
title: Coverting Illumina IDAT to VCF/PLINK BINARY
layout: pages
---

**Content**

1. [Requirements](#requirements)
2. [Step-by-Step procedure](#procedure)

## Requirements

1. Illumina Array Analysis Platform Genotyping Command Line (iaap-cl)

2. The gtc2vcf bcftools plugin

3. Manifest and cluster files for the chip used to generate your IDAT files
   - The manifest for the chip used to generate your data should typically be provided to you
   - If you used the **H3Africa chip**, these files can be downloaded from [here](https://chipinfo.h3abionet.org/downloads) 
   - You can find more resources from the Illumina website [here](https://emea.support.illumina.com/array/downloads.html)

## Step-by-step procedure <a name="procedure"></a>

1. Download iaap-cli

   - This can be downloaded from [here](https://emea.support.illumina.com/downloads/iaap-genotyping-cli.html)

     **Note** You need to create an account, and then you can download it freely.

   - Alternatively, you can run the code below (linux). This was adapted from https://github.com/freeseek/gtc2vcf

   Mac user may replace ```wget``` with ```curl``` or an equivalent of the packages

```
# Linux users
wget ftp://webdata2:webdata2@ussd-ftp.illumina.com/downloads/software/iaap/iaap-cli-linux-x64-1.1.0.tar.gz

# Mac users
curl ftp://webdata2:webdata2@ussd-ftp.illumina.com/downloads/software/iaap/iaap-cli-linux-x64-1.1.0.tar.gz --output iaap-cli-linux-x64-1.1.0.tar.gz
```

2. Install iaap-cli

   The following instructions have been adapted from https://github.com/freeseek/gtc2vcf. 
   You may visit the github page for further useful information

```
# setup some relevant paths
mkdir -p $HOME/bin && cd /tmp

# Extract and place iaap-cli in the relevant paths
tar xzvf iaap-cli-linux-x64-1.1.0.tar.gz -C $HOME/bin/ iaap-cli-linux-x64-1.1.0/iaap-cli --strip-components=1
```

3. Get a pre-compiled binary of bcftools containing the gtc2vcf plugin

```
# Linux users
wget https://software.broadinstitute.org/software/gtc2vcf/gtc2vcf_1.15.1-20220518.zip

# Mac users
curl https://software.broadinstitute.org/software/gtc2vcf/gtc2vcf_1.15.1-20220518.zip --output gtc2vcf_1.15.1-20220518.zip
```


