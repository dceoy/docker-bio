docker-bio
==========

Dockerfile repository for Bioinformatics

[![CI to Docker Hub](https://github.com/dceoy/docker-bio/actions/workflows/docker-publish.yml/badge.svg)](https://github.com/dceoy/docker-bio/actions/workflows/docker-publish.yml)

Docker images
-------------

- Images on Docker Hub:
  - [abra2](https://hub.docker.com/r/dceoy/abra2/)
  - [alfred](https://hub.docker.com/r/dceoy/alfred/)
  - [ascat](https://hub.docker.com/r/dceoy/ascat/)
  - [bamsnap](https://hub.docker.com/r/dceoy/bamsnap/)
  - [bcftools](https://hub.docker.com/r/dceoy/bcftools/)
  - [bedops](https://hub.docker.com/r/dceoy/bedops/)
  - [bedtools](https://hub.docker.com/r/dceoy/bedtools/)
  - [bioconda](https://hub.docker.com/r/dceoy/bioconda/)
  - [bowtie2](https://hub.docker.com/r/dceoy/bowtie2/)
  - [bwa](https://hub.docker.com/r/dceoy/bwa/)
  - [bwa-mem2](https://hub.docker.com/r/dceoy/bwa-mem2/)
  - [cufflinks](https://hub.docker.com/r/dceoy/cufflinks/)
  - [cnvkit](https://hub.docker.com/r/dceoy/cnvkit/)
  - [cnvnator](https://hub.docker.com/r/dceoy/cnvnator/)
  - [cutadapt](https://hub.docker.com/r/dceoy/cutadapt/)
  - [delly](https://hub.docker.com/r/dceoy/delly/)
  - [dicey](https://hub.docker.com/r/dceoy/dicey/)
  - [elprep](https://hub.docker.com/r/dceoy/elprep/)
  - [fastp](https://hub.docker.com/r/dceoy/fastp/)
  - [fastq-dump](https://hub.docker.com/r/dceoy/fastq-dump/)
  - [fastqc](https://hub.docker.com/r/dceoy/fastqc/)
  - [fgbio](https://hub.docker.com/r/dceoy/fgbio/)
  - [freec](https://hub.docker.com/r/dceoy/freec/)
  - [gatk](https://hub.docker.com/r/dceoy/gatk/)
  - [gencore](https://hub.docker.com/r/dceoy/gencore/)
  - [gffread](https://hub.docker.com/r/dceoy/gffread/)
  - [gridss](https://hub.docker.com/r/dceoy/gridss/)
  - [goleft](https://hub.docker.com/r/dceoy/goleft/)
  - [hisat2](https://hub.docker.com/r/dceoy/hisat2/)
  - ~igv~
  - [igv-webapp](https://hub.docker.com/r/dceoy/igv-webapp/)
  - [jbrowse](https://hub.docker.com/r/dceoy/jbrowse/)
  - [kallisto](https://hub.docker.com/r/dceoy/kallisto/)
  - ~last~
  - [lumpy](https://hub.docker.com/r/dceoy/lumpy/)
  - [macs2](https://hub.docker.com/r/dceoy/macs2/)
  - [manta](https://hub.docker.com/r/dceoy/manta/)
  - [miso](https://hub.docker.com/r/dceoy/miso/)
  - [msisensor](https://hub.docker.com/r/dceoy/msisensor/)
  - [msisensor-pro](https://hub.docker.com/r/dceoy/msisensor-pro/)
  - [multiqc](https://hub.docker.com/r/dceoy/multiqc/)
  - [nirvana](https://hub.docker.com/r/dceoy/nirvana/)
  - ~oncotator~
  - [picard](https://hub.docker.com/r/dceoy/picard/)
  - ~pindel~
  - [prinseq](https://hub.docker.com/r/dceoy/prinseq/)
  - [rsem](https://hub.docker.com/r/dceoy/rsem/)
  - [sambamba](https://hub.docker.com/r/dceoy/sambamba/)
  - [samplot](https://hub.docker.com/r/dceoy/samplot/)
  - [samtools](https://hub.docker.com/r/dceoy/samtools/)
  - [seqkit](https://hub.docker.com/r/dceoy/seqkit/)
  - [sequenza](https://hub.docker.com/r/dceoy/sequenza/)
  - [sigprofiler](https://hub.docker.com/r/dceoy/sigprofiler/)
  - ~smoove~
  - [snpeff](https://hub.docker.com/r/dceoy/snpeff/)
  - [star](https://hub.docker.com/r/dceoy/star/)
  - [strelka](https://hub.docker.com/r/dceoy/strelka/)
  - [svtools](https://hub.docker.com/r/dceoy/svtools/)
  - [trim_galore](https://hub.docker.com/r/dceoy/trim_galore/)
  - [trimmomatic](https://hub.docker.com/r/dceoy/trimmomatic/)
  - [varscan](https://hub.docker.com/r/dceoy/varscan/)
  - [vep](https://hub.docker.com/r/dceoy/vep/)
- Images requiring a user build:
  - annovar
  - bcl2fastq
- Images outside this repository:
  - [deepvariant](https://console.cloud.google.com/gcr/images/deepvariant-docker/GLOBAL/deepvariant)
  - [deepvariant_gpu](https://console.cloud.google.com/gcr/images/deepvariant-docker/GLOBAL/deepvariant_gpu)

Docker Compose
--------------

- Pull an image

  ```sh
  $ docker-compose pull <name>
  ```

- Build an image

  ```sh
  $ docker-compose build <name>
  ```

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

References
----------

- abra2
  - [GitHub - mozack/abra2](https://github.com/mozack/abra2)
- alfred
  - [GitHub - tobiasrausch/alfred](https://github.com/tobiasrausch/alfred)
  - [www.gear-genomics.com - Alfred](https://www.gear-genomics.com/docs/alfred/)
- annovar
  - [annovar.openbioinformatics.org - ANNOVAR](http://annovar.openbioinformatics.org/)
- ascat
  - [GitHub - Crick-CancerGenomics/ascat](https://github.com/Crick-CancerGenomics/ascat)
  - [The Francis Crick Institute - Allele-Specific Copy number Analysis of Tumours (ASCAT)](https://www.crick.ac.uk/research/labs/peter-van-loo/software)
- bamsnap
  - [bamsnap.readthedocs.io - BamSnap](https://bamsnap.readthedocs.io/en/latest/)
  - [GitHub - parklab/bamsnap](https://github.com/parklab/bamsnap)
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
- bwa-mem2
  - [GitHub - bwa-mem2/bwa-mem2](https://github.com/bwa-mem2/bwa-mem2)
- canvas
  - [GitHub - Illumina/canvas](https://github.com/Illumina/canvas)
- cn.mops
  - [Bioconductor - cn.mops](https://bioconductor.org/packages/release/bioc/html/cn.mops.html)
- cnvkit
  - [cnvkit.readthedocs.io - CNVkit](https://cnvkit.readthedocs.io/)
  - [GitHub - etal/cnvkit](https://github.com/etal/cnvkit)
- cufflinks
  - [Trapnell Lab - Cufflinks](http://cole-trapnell-lab.github.io/cufflinks/)
  - [GitHub - cole-trapnell-lab/cufflinks](https://github.com/cole-trapnell-lab/cufflinks)
- cutadapt
  - [cutadapt.readthedocs.io - Cutadapt](http://cutadapt.readthedocs.io/)
  - [GitHub - marcelm/cutadapt](https://github.com/marcelm/cutadapt)
- deepvariant
  - [GitHub -google/deepvariant](https://github.com/google/deepvariant)
  - [Google Cloud Platform - DeepVariant](https://cloud.google.com/genomics/deepvariant)
- delly
  - [GitHub - dellytools/delly](https://github.com/dellytools/delly)
- dicey
  - [GitHub - gear-genomics/dicey](https://github.com/gear-genomics/dicey)
- elprep
  - [GitHub - ExaScience/elprep](https://github.com/ExaScience/elprep)
- fastp
  - [GitHub - OpenGene/fastp](https://github.com/OpenGene/fastp#per-read-cutting-by-quality-score)
- fastq-dump
  - [NCBI - SRA Toolkit](https://www.ncbi.nlm.nih.gov/books/NBK158900/)
- fastqc
  - [Babraham Bioinformatics - FastQC](http://www.bioinformatics.babraham.ac.uk/projects/fastqc/)
- fgbio
  - [GitHub - fulcrumgenomics/fgbio](https://github.com/fulcrumgenomics/fgbio)
  - [fulcrumgenomics.github.io - fgbio](http://fulcrumgenomics.github.io/fgbio/)
- freec
  - [boevalab.inf.ethz.ch - Control-FREEC](http://boevalab.inf.ethz.ch/FREEC/index.html)
  - [GitHub - BoevaLab/FREEC](https://github.com/BoevaLab/FREEC)
- gatk
  - [Broad Institute - Genome Analysis Toolkit](https://software.broadinstitute.org/gatk/)
  - [GitHub - broadinstitute/gatk](https://github.com/broadinstitute/gatk)
- gencore
  - [GitHub - OpenGene/gencore](https://github.com/OpenGene/gencore)
- gffread
  - [GitHub - gpertea/gffread](https://github.com/gpertea/gffread)
- gridss
  - [GitHub - PapenfussLab/gridss](https://github.com/PapenfussLab/gridss)
- goleft
  - [GitHub - brentp/goleft](https://github.com/brentp/goleft)
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
- kallisto
  - [pachterlab.github.io - kallisto](https://pachterlab.github.io/kallisto/)
  - [GitHub - pachterlab/kallisto](https://github.com/pachterlab/kallisto)
- last
  - [last.cbrc.jp - LAST](http://last.cbrc.jp/)
- lumpy
  - [GitHub - arq5x/lumpy-sv](https://github.com/arq5x/lumpy-sv)
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
- msisensor-pro
  - [GitHub - xjtu-omics/msisensor-pro](https://github.com/xjtu-omics/msisensor-pro)
- multiqc
  - [GitHub - ewels/MultiQC](https://github.com/ewels/MultiQC)
- nirvana
  - [GitHub - Illumina/Nirvana](https://github.com/Illumina/Nirvana)
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
- sambamba
  - [GitHub - biod/sambamba](https://github.com/biod/sambamba)
  - [lomereiter.github.io - Sambamba](https://lomereiter.github.io/sambamba/)
- samplot
  - [GitHub - ryanlayer/samplot](https://github.com/ryanlayer/samplot)
- samtools
  - [samtools.sourceforge.net - SAMtools](http://samtools.sourceforge.net/)
  - [GitHub - samtools/samtools](https://github.com/samtools/samtools)
- seqkit
  - [bioinf.shenwei.me - SeqKit](https://bioinf.shenwei.me/seqkit/)
  - [GitHub - shenwei356/seqkit](https://github.com/shenwei356/seqkit/)
- sequenza
  - [CRAN - sequenza](https://cran.r-project.org/web/packages/sequenza/)
  - [sequenzatools.bitbucket.io - Sequenza](https://sequenzatools.bitbucket.io/)
  - [Bitbucket - Sequenza](https://bitbucket.org/sequenzatools/sequenza/)
  - [Bitbucket - Sequenza-utils](https://bitbucket.org/sequenzatools/sequenza-utils/)
  - [sequenza-utils.readthedocs.io - Sequenza-utils](https://sequenza-utils.readthedocs.io/)
- sigprofiler
  - [COSMIC Mutational Signatures - SigProfiler Tools](https://cancer.sanger.ac.uk/cosmic/signatures/sigprofiler.tt)
  - [GitHub - AlexandrovLab/SigProfilerMatrixGenerator](https://github.com/AlexandrovLab/SigProfilerMatrixGenerator)
  - [GitHub - AlexandrovLab/SigProfilerPlotting](https://github.com/AlexandrovLab/SigProfilerPlotting)
  - [GitHub - AlexandrovLab/SigProfilerExtractor](https://github.com/AlexandrovLab/SigProfilerExtractor)
  - [GitHub - AlexandrovLab/SigProfilerSimulator](https://github.com/AlexandrovLab/SigProfilerSimulator)
- smoove
  - [GitHub - brentp/smoove](https://github.com/brentp/smoove)
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
- vep
  - [www.ensembl.org - Ensembl Variant Effect Predictor (VEP)](https://www.ensembl.org/vep)
  - [GitHub - Ensembl/ensembl-vep](https://github.com/Ensembl/ensembl-vep)
