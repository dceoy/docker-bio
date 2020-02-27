docker-bio
==========

Dockerfile repository for Bioinformatics

Docker images
-------------

- Images on Docker Hub:
  - [abra2](https://hub.docker.com/r/dceoy/abra2/)
  - [ascat](https://hub.docker.com/r/dceoy/ascat/)
  - [bcftools](https://hub.docker.com/r/dceoy/bcftools/)
  - [bedops](https://hub.docker.com/r/dceoy/bedops/)
  - [bedtools](https://hub.docker.com/r/dceoy/bedtools/)
  - [bioconda](https://hub.docker.com/r/dceoy/bioconda/)
  - [bowtie2](https://hub.docker.com/r/dceoy/bowtie2/)
  - [bwa](https://hub.docker.com/r/dceoy/bwa/)
  - [cufflinks](https://hub.docker.com/r/dceoy/cufflinks/)
  - [cnvnator](https://hub.docker.com/r/dceoy/cnvnator/)
  - [cutadapt](https://hub.docker.com/r/dceoy/cutadapt/)
  - [delly](https://hub.docker.com/r/dceoy/delly/)
  - [elprep](https://hub.docker.com/r/dceoy/elprep/)
  - [fastq-dump](https://hub.docker.com/r/dceoy/fastq-dump/)
  - [fastqc](https://hub.docker.com/r/dceoy/fastqc/)
  - [fgbio](https://hub.docker.com/r/dceoy/fgbio/)
  - [gatk](https://hub.docker.com/r/dceoy/gatk/)
  - [gencore](https://hub.docker.com/r/dceoy/gencore/)
  - [hisat2](https://hub.docker.com/r/dceoy/hisat2/)
  - ~igv~
  - [igv-webapp](https://hub.docker.com/r/dceoy/igv-webapp/)
  - [jbrowse](https://hub.docker.com/r/dceoy/jbrowse/)
  - [last](https://hub.docker.com/r/dceoy/last/)
  - [macs2](https://hub.docker.com/r/dceoy/macs2/)
  - [manta](https://hub.docker.com/r/dceoy/manta/)
  - [miso](https://hub.docker.com/r/dceoy/miso/)
  - [msisensor](https://hub.docker.com/r/dceoy/msisensor/)
  - ~oncotator~
  - [picard](https://hub.docker.com/r/dceoy/picard/)
  - ~pindel~
  - [prinseq](https://hub.docker.com/r/dceoy/prinseq/)
  - [rsem](https://hub.docker.com/r/dceoy/rsem/)
  - [samtools](https://hub.docker.com/r/dceoy/samtools/)
  - [snpeff](https://hub.docker.com/r/dceoy/snpeff/)
  - [star](https://hub.docker.com/r/dceoy/star/)
  - [strelka](https://hub.docker.com/r/dceoy/strelka/)
  - [svtools](https://hub.docker.com/r/dceoy/svtools/)
  - [trim_galore](https://hub.docker.com/r/dceoy/trim_galore/)
  - [trimmomatic](https://hub.docker.com/r/dceoy/trimmomatic/)
  - [varscan](https://hub.docker.com/r/dceoy/varscan/)
- Images requiring a user build:
  - annovar
  - bcl2fastq
- Images outside this repository:
  - [deepvariant](https://console.cloud.google.com/gcr/images/deepvariant-docker/GLOBAL/deepvariant)
  - [deepvariant_gpu](https://console.cloud.google.com/gcr/images/deepvariant-docker/GLOBAL/deepvariant_gpu)

References
----------

- abra2
  - [GitHub - mozack/abra2](https://github.com/mozack/abra2)
- annovar
  - [annovar.openbioinformatics.org - ANNOVAR](http://annovar.openbioinformatics.org/)
- ascat
  - [GitHub - Crick-CancerGenomics/ascat](https://github.com/Crick-CancerGenomics/ascat)
  - [The Francis Crick Institute - Allele-Specific Copy number Analysis of Tumours (ASCAT)](https://www.crick.ac.uk/research/labs/peter-van-loo/software)
- bcftools
  - [samtools.github.io - Bcftools](https://samtools.github.io/bcftools/)
  - [GitHub - samtools/bcftools](https://github.com/samtools/bcftools)
- bcl2fastq
  - [Illumina - bcl2fastq Conversion Software](https://support.illumina.com/sequencing/sequencing_software/bcl2fastq-conversion-software.html)
- bedops
  - [bedops.readthedocs.io - BEDOPS](https://bedops.readthedocs.io/)
  - [GitHub - bedops/bedops](https://github.com/bedops/bedops)
- bedtools
  - [bedtools.readthedocs.io - bedtools2](http://bedtools.readthedocs.io/en/latest/index.html)
  - [GitHub - arq5x/bedtools2](https://github.com/arq5x/bedtools2)
- bioconda
  - [bioconda.github.io - Bioconda](https://bioconda.github.io/)
- bowtie2
  - [bowtie-bio.sourceforge.net - Bowtie 2](http://bowtie-bio.sourceforge.net/bowtie2/index.shtml)
  - [GitHub - BenLangmead/bowtie2](https://github.com/BenLangmead/bowtie2)
- bwa
  - [bio-bwa.sourceforge.net - Burrows-Wheeler Aligner](http://bio-bwa.sourceforge.net/)
  - [GitHub - lh3/bwa](https://github.com/lh3/bwa)
- cnvnator
  - [GitHub - abyzovlab/cnvnator](https://github.com/abyzovlab/cnvnator)
- cufflinks
  - [Trapnell Lab - Cufflinks](http://cole-trapnell-lab.github.io/cufflinks/)
  - [GitHub - cole-trapnell-lab/cufflinks](https://github.com/cole-trapnell-lab/cufflinks)
- cutadapt
  - [cutadapt.readthedocs.io - cutadapt](http://cutadapt.readthedocs.io/)
  - [GitHub - marcelm/cutadapt](https://github.com/marcelm/cutadapt)
- deepvariant
  - [GitHub -google/deepvariant](https://github.com/google/deepvariant)
  - [Google Cloud Platform - DeepVariant](https://cloud.google.com/genomics/deepvariant)
- delly
  - [GitHub - dellytools/delly](https://github.com/dellytools/delly)
- elprep
  - [GitHub - ExaScience/elprep](https://github.com/ExaScience/elprep)
- fastq-dump
  - [NCBI - SRA Toolkit](https://www.ncbi.nlm.nih.gov/books/NBK158900/)
- fastqc
  - [Babraham Bioinformatics - FastQC](http://www.bioinformatics.babraham.ac.uk/projects/fastqc/)
- fgbio
  - [GitHub - fulcrumgenomics/fgbio](https://github.com/fulcrumgenomics/fgbio)
  - [fulcrumgenomics.github.io - fgbio](http://fulcrumgenomics.github.io/fgbio/)
- gatk
  - [Broad Institute - Genome Analysis Toolkit](https://software.broadinstitute.org/gatk/)
  - [GitHub - broadinstitute/gatk](https://github.com/broadinstitute/gatk)
- gencore
  - [GitHub - OpenGene/gencore](https://github.com/OpenGene/gencore)
- hisat2
  - [Johns Hopkins University - HISAT2](http://ccb.jhu.edu/software/hisat2/)
  - [GitHub - infphilo/hisat2](https://github.com/infphilo/hisat2)
- igv:
  - [Broad Institute - Integrative Genomics Viewer](https://igv.org/)
  - [GitHub - igvteam/igv](https://github.com/igvteam/igv)
- igv-webapp:
  - [Broad Institute - Integrative Genomics Viewer](https://igv.org/)
  - [GitHub - igvteam/igv-webapp](https://github.com/igvteam/igv-webapp)
- jbrowse
  - [jbrowse.org - The JBrowse Genome Browser](http://jbrowse.org/)
  - [GitHub - GMOD/jbrowse](https://github.com/GMOD/jbrowse)
- last
  - [last.cbrc.jp - LAST](http://last.cbrc.jp/)
- macs2
  - [X. Shirley Liu Lab - MACS](http://liulab.dfci.harvard.edu/MACS/)
  - [GitHub - taoliu/MACS](https://github.com/taoliu/MACS)
- manta
  - [GitHub - Illumina/manta](https://github.com/Illumina/manta)
- miso
  - [miso.readthedocs.io - MISO](https://miso.readthedocs.io/en/fastmiso/)
  - [hollywood.mit.edu - MISO](http://hollywood.mit.edu/burgelab/miso/index.html)
  - [GitHub - yarden/MISO](https://github.com/yarden/MISO)
- msisensor
  - [GitHub - ding-lab/msisensor](https://github.com/ding-lab/msisensor)
- oncotator
  - [Broad Institute - Oncotator](http://portals.broadinstitute.org/oncotator/)
  - [GitHub - broadinstitute/oncotator](https://github.com/broadinstitute/oncotator)
- picard
  - [broadinstitute.github.io - Picard](https://broadinstitute.github.io/picard/)
  - [GitHub - broadinstitute/picard](https://github.com/broadinstitute/picard)
- pindel
  - [GitHub - genome/pindel](https://github.com/genome/pindel)
- prinseq
  - [prinseq.sourceforge.net - PRINSEQ](http://prinseq.sourceforge.net/)
- rsem
  - [deweylab.github.io - RSEM (RNA-Seq by Expectation-Maximization)](https://deweylab.github.io/RSEM/)
  - [GitHub - deweylab/RSEM](https://github.com/deweylab/RSEM)
- samtools
  - [samtools.sourceforge.net - SAMtools](http://samtools.sourceforge.net/)
  - [GitHub - samtools/samtools](https://github.com/samtools/samtools)
- snpeff
  - [snpeff.sourceforge.net - SnpEff](http://snpeff.sourceforge.net/index.html)
- star
  - [GitHub - alexdobin/STAR](https://github.com/alexdobin/STAR)
- strelka
  - [GitHub - Illumina/strelka](https://github.com/Illumina/strelka)
- svtools
  - [GitHub - hall-lab/svtools](https://github.com/hall-lab/svtools)
- trim_galore
  - [GitHub - FelixKrueger/TrimGalore](https://github.com/FelixKrueger/TrimGalore)
  - [Babraham Bioinformatics - Trim Galore](https://www.bioinformatics.babraham.ac.uk/projects/trim_galore/)
- trimmomatic
  - [usadellab.org - Trimmomatic](http://www.usadellab.org/cms/?page=trimmomatic)
  - [GitHub - timflutre/trimmomatic](https://github.com/timflutre/trimmomatic)
- varscan
  - [massgenomics.org - VarScan](http://massgenomics.org/varscan)
  - [dkoboldt.github.io - VarScan](http://dkoboldt.github.io/varscan/)
  - [GitHub - dkoboldt/varscan](https://github.com/dkoboldt/varscan)

Dependencies
------------

Some images use the following tools:

- print-github-tags
  - Tiny command to fetch repository tags or releases from GitHub
  - [GitHub - dceoy/print-github-tags](https://github.com/dceoy/print-github-tags)
- clir
  - R package manager for command line interface
  - [GitHub - dceoy/clir](https://github.com/dceoy/clir)
  - [DockerHub - dceoy/clir](https://hub.docker.com/r/dceoy/clir)
