# *Vagococcus spp.*

#### Overlapping Paired-End Illumina Reads
Although all isolates were sequenced with paired-end Illumina (2x250 bp), many reads appeared to overlap, so this was a good time to test different methods on 8 different but related species of *Vagococcus*.

`brew install bbtools flash pear spades trimmomatic quast`

- none, no overlapping performed
- FLASH v1.2.11: 10.1093/bioinformatics/btr507
- PEAR v0.9.10: 10.1093/bioinformatics/btt593
- PandaSeq (not included here) 10.1186/1471-2105-13-31. Non-overlapping reads lose their read numbers (1, 2) field in the FastQ e.g., `pandaseq -f R1.fastq.gz -r R2.fastq.gz -F -o 10 -O 251 -T 32 -U unmerged.fq -w merged.fastq` and consequently the power of paired-end sequencing/assembly is removed.

All reads were cleaned the same way. Paired as well as singleton reads were passed to SPAdes v3.9.0 `--only-assembler --cov-cutoff auto` with contigs at least 1 kb in size assessed in QUAST v4.2.

When reads are not overlapped prior to assembly, SPAdes never (0 of 8, 0%) gave the warning, *"Estimated mean insert size < FLOAT > is very small compared to read length < INT >."* However, 28 of 32 (87.5%) instances where overlapping reads were resolved and given as singletons to SPAdes logs this warning.

|Sample ID|Overlap Method|Contigs [#]|Largest contig [bp]|Total length [bp]|GC [%]|N50|Unique genes [#]|Genes >= 300 bp [#]
|---------|----------------------------|-----------|-------------------|-----------------|-----|-------|----------------|-------------------
|339|none|28|362160|2653706|32.41|184402|2622|2362
|339|flash -M 251 --min-overlap=10|27|376297|2653661|32.41|184402|2621|2361
|339|flash -M 251 --min-overlap=15|26|376297|2653784|32.41|274101|2621|2361
|339|pear -k --min-overlap 10|27|376297|2653378|32.41|184402|2621|2361
|339|pear -k --min-overlap 15|26|376297|2653580|32.41|274180|2620|2361
|340|none|45|340743|3104446|37.55|115236|2913|2647
|340|flash -M 251 --min-overlap=10|50|340743|3102834|37.55|115236|2915|2650
|340|flash -M 251 --min-overlap=15|50|340743|3102838|37.55|115236|2915|2650
|340|pear -k --min-overlap 10|49|340581|3102539|37.55|115236|2915|2649
|340|pear -k --min-overlap 15|49|340581|3102543|37.55|115236|2914|2649
|565|none|22|344184|1992244|37.62|141567|1854|1731
|565|flash -M 251 --min-overlap=10|23|270912|1991926|37.62|141567|1854|1735
|565|flash -M 251 --min-overlap=15|23|270912|1991926|37.62|141567|1855|1734
|565|pear -k --min-overlap 10|22|343311|1991552|37.62|141411|1856|1734
|565|pear -k --min-overlap 15|22|343311|1991552|37.62|141411|1856|1734
|709|none|8|899127|2257832|35.36|823406|2140|1952
|709|flash -M 251 --min-overlap=10|8|898890|2257337|35.36|823148|2140|1952
|709|flash -M 251 --min-overlap=15|8|898890|2257106|35.36|822917|2139|1952
|709|pear -k --min-overlap 10|9|898890|2255817|35.36|642903|2142|1953
|709|pear -k --min-overlap 15|9|898890|2255851|35.36|642903|2140|1953
|714|none|37|378669|3080929|32.55|191814|2971|2691
|714|flash -M 251 --min-overlap=10|37|378669|3081454|32.55|191814|2971|2693
|714|flash -M 251 --min-overlap=15|37|378669|3081454|32.55|191814|2971|2692
|714|pear -k --min-overlap 10|38|378669|3080743|32.55|191814|2972|2694
|714|pear -k --min-overlap 15|38|378669|3080743|32.55|191814|2972|2693
|853|none|40|444425|2862533|44.34|155062|2766|2467
|853|flash -M 251 --min-overlap=10|41|351340|2857409|44.34|134873|2757|2460
|853|flash -M 251 --min-overlap=15|41|351340|2857360|44.34|134873|2757|2460
|853|pear -k --min-overlap 10|42|351340|2857009|44.34|134873|2756|2461
|853|pear -k --min-overlap 15|42|351340|2857330|44.34|134873|2757|2461
|854|none|52|179153|2336491|34.99|124556|2199|1986
|854|flash -M 251 --min-overlap=10|50|179153|2331242|34.96|124556|2198|1986
|854|flash -M 251 --min-overlap=15|50|179153|2331251|34.96|124556|2198|1986
|854|pear -k --min-overlap 10|50|179153|2331382|34.97|124556|2198|1986
|854|pear -k --min-overlap 15|51|179153|2332238|34.97|124556|2199|1985
|933|none|7|1260240|2444868|36.48|1260240|2351|2059
|933|flash -M 251 --min-overlap=10|8|1260240|2444805|36.48|1260240|2348|2058
|933|flash -M 251 --min-overlap=15|7|1260240|2444844|36.48|1260240|2348|2057
|933|pear -k --min-overlap 10|9|1260234|2441908|36.46|1260234|2351|2058
|933|pear -k --min-overlap 15|8|1260234|2441857|36.46|1260234|2350|2057
