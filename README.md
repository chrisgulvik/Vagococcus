# *Vagococcus spp.*
- *Vagococcus:* wandering coccus, referring to motility

#### Overlapping Paired-End Illumina Reads
Although all isolates were sequenced with paired-end Illumina (2x250 bp), many reads appeared to overlap, so this was a good time to test different methods on 9 different but related species of *Vagococcus*.

`brew install bbtools flash pear spades trimmomatic quast`

- none, no overlapping performed
- FLASH v1.2.11: [10.1093/bioinformatics/btr507](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3198573/)
- PEAR v0.9.10: [10.1093/bioinformatics/btt593](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3933873/)
- PandaSeq (not included here) [10.1186/1471-2105-13-31](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3471323/). Non-overlapping reads lose their read numbers (1, 2) field in the FastQ e.g., `pandaseq -f R1.fastq.gz -r R2.fastq.gz -F -o 10 -O 251 -T 32 -U unmerged.fq -w merged.fastq` and consequently the power of paired-end sequencing/assembly is removed.

All reads were cleaned the same way. Paired as well as singleton reads were passed to SPAdes v3.9.0 `--only-assembler --cov-cutoff auto` with contigs at least 1 kb in size assessed in QUAST v4.2.

When reads are not overlapped prior to assembly, SPAdes never (0 of 9, 0%) gave the warning, *"Estimated mean insert size < FLOAT > is very small compared to read length < INT >."* However, 80 of 90 (88.9%) instances where overlapping reads were resolved and given as singletons to SPAdes logs this warning. All overlap methods (10 of 10) for sample 339 lacked a warning, so it likely does not have however all other overlap methods with the remaining 8 samples (80 of 80) gave the warning.

|Sample ID|Overlap Method|Contigs [#]|Largest contig [bp]|Total length [bp]|GC [%]|N50|Unique genes [#]|Genes >= 300 bp [#]
|---------|----------------------------|-----------|-------------------|-----------------|-----|-------|----------------|-------------------
|339<sup>**a**</sup>|none|28|362160|2653706|32.41|184402|2622|2362
|339<sup>**a**</sup>|flash -M 300 --min-overlap=10|27|376297|2653661|32.41|184402|2621|2361
|339<sup>**a**</sup>|flash -M 300 --min-overlap=15|26|376297|2653784|32.41|274101|2621|2361
|339<sup>**a**</sup>|flash -M 300 --min-overlap=20|26|376297|2653784|32.41|274101|2621|2361
|339<sup>**a**</sup>|flash -M 300 --min-overlap=25|27|376297|2653661|32.41|184402|2622|2361
|339<sup>**a**</sup>|flash -M 300 --min-overlap=30|27|376297|2653661|32.41|184402|2622|2361
|339<sup>**a**</sup>|pear -k --min-overlap 10|27|376297|2653378|32.41|184402|2621|2361
|339<sup>**a**</sup>|pear -k --min-overlap 15|26|376297|2653580|32.41|274180|2620|2361
|339<sup>**a**</sup>|pear -k --min-overlap 20|26|376297|2653580|32.41|274180|2620|2361
|339<sup>**a**</sup>|pear -k --min-overlap 25|27|376297|2653457|32.41|184402|2621|2361
|339<sup>**a**</sup>|pear -k --min-overlap 30|27|376297|2653615|32.41|184402|2621|2361
|340<sup>**a**</sup>|none|45|340743|3104446|37.55|115236|2913|2647
|340|flash -M 300 --min-overlap=10|50|340743|3102834|37.55|115236|2915|2650
|340|flash -M 300 --min-overlap=15|50|340743|3102838|37.55|115236|2915|2650
|340|flash -M 300 --min-overlap=20|50|340743|3102887|37.55|115236|2914|2649
|340|flash -M 300 --min-overlap=25|50|340743|3103336|37.55|115236|2916|2650
|340|flash -M 300 --min-overlap=30|50|340743|3103336|37.55|115236|2916|2650
|340|pear -k --min-overlap 10|49|340581|3102539|37.55|115236|2915|2649
|340|pear -k --min-overlap 15|49|340581|3102543|37.55|115236|2914|2649
|340|pear -k --min-overlap 20|49|340581|3102543|37.55|115236|2915|2649
|340|pear -k --min-overlap 25|49|340581|3102543|37.55|115236|2914|2650
|340|pear -k --min-overlap 30|52|281558|3092755|37.55|115236|2914|2642
|565<sup>**a**</sup>|none|22|344184|1992244|37.62|141567|1854|1731
|565|flash -M 300 --min-overlap=10|23|270912|1991926|37.62|141567|1854|1735
|565|flash -M 300 --min-overlap=15|23|270912|1991926|37.62|141567|1855|1734
|565|flash -M 300 --min-overlap=20|23|270912|1991926|37.62|141567|1854|1735
|565|flash -M 300 --min-overlap=25|23|270912|1991926|37.62|141567|1855|1734
|565|flash -M 300 --min-overlap=30|23|270912|1991926|37.62|141567|1855|1734
|565|pear -k --min-overlap 10|22|343311|1991552|37.62|141411|1856|1734
|565|pear -k --min-overlap 15|22|343311|1991552|37.62|141411|1856|1734
|565|pear -k --min-overlap 20|22|343311|1991552|37.62|141411|1856|1734
|565|pear -k --min-overlap 25|22|343311|1991551|37.62|141411|1857|1733
|565|pear -k --min-overlap 30|22|343311|1991551|37.62|141411|1856|1734
|709<sup>**a**</sup>|none|8|899127|2257832|35.36|823406|2140|1952
|709|flash -M 300 --min-overlap=10|8|898890|2257337|35.36|823148|2140|1952
|709|flash -M 300 --min-overlap=15|8|898890|2257106|35.36|822917|2139|1952
|709|flash -M 300 --min-overlap=20|8|898890|2257106|35.36|822917|2139|1952
|709|flash -M 300 --min-overlap=25|8|898890|2257106|35.36|822917|2140|1952
|709|flash -M 300 --min-overlap=30|8|898890|2257106|35.36|822917|2140|1952
|709|pear -k --min-overlap 10|9|898890|2255817|35.36|642903|2142|1953
|709|pear -k --min-overlap 15|9|898890|2255851|35.36|642903|2140|1953
|709|pear -k --min-overlap 20|9|898890|2255851|35.36|642903|2141|1953
|709|pear -k --min-overlap 25|9|898890|2255851|35.36|642903|2140|1953
|709|pear -k --min-overlap 30|9|898890|2255851|35.36|642903|2140|1953
|714<sup>**a**</sup>|none|37|378669|3080929|32.55|191814|2971|2691
|714|flash -M 300 --min-overlap=10|37|378669|3081454|32.55|191814|2971|2693
|714|flash -M 300 --min-overlap=15|37|378669|3081454|32.55|191814|2971|2692
|714|flash -M 300 --min-overlap=20|37|378669|3081454|32.55|191814|2971|2692
|714|flash -M 300 --min-overlap=25|37|378669|3081454|32.55|191814|2971|2692
|714|flash -M 300 --min-overlap=30|37|378669|3080929|32.55|191814|2971|2691
|714|pear -k --min-overlap 10|38|378669|3080743|32.55|191814|2972|2694
|714|pear -k --min-overlap 15|38|378669|3080743|32.55|191814|2972|2693
|714|pear -k --min-overlap 20|38|378669|3080743|32.55|191814|2972|2693
|714|pear -k --min-overlap 25|38|378669|3080743|32.55|191814|2972|2694
|714|pear -k --min-overlap 30|38|378669|3080218|32.55|191814|2972|2693
|822<sup>**a**</sup>|none|55|310847|2879210|38.14|122341|2722|2393
|822|flash -M 300 --min-overlap=10|62|310846|2876328|38.14|120625|2728|2393
|822|flash -M 300 --min-overlap=15|60|310846|2876065|38.14|120625|2728|2394
|822|flash -M 300 --min-overlap=20|61|310846|2878557|38.14|120629|2730|2396
|822|flash -M 300 --min-overlap=25|61|310846|2877785|38.14|120629|2729|2395
|822|flash -M 300 --min-overlap=30|60|310846|2876804|38.14|120629|2725|2394
|822|pear -k --min-overlap 10|68|310846|2868847|38.13|112648|2726|2396
|822|pear -k --min-overlap 15|67|310846|2870732|38.13|112648|2727|2398
|822|pear -k --min-overlap 20|68|310846|2872765|38.13|113712|2731|2400
|822|pear -k --min-overlap 25|67|310846|2872609|38.13|113712|2732|2401
|822|pear -k --min-overlap 30|65|310846|2871366|38.13|116461|2726|2398
|853<sup>**a**</sup>|none|40|444425|2862533|44.34|155062|2766|2467
|853|flash -M 300 --min-overlap=10|41|351340|2857409|44.34|134873|2757|2460
|853|flash -M 300 --min-overlap=15|41|351340|2857360|44.34|134873|2757|2460
|853|flash -M 300 --min-overlap=20|41|351340|2858195|44.34|138191|2760|2462
|853|flash -M 300 --min-overlap=25|41|444200|2859392|44.35|155912|2760|2462
|853|flash -M 300 --min-overlap=30|39|444200|2859691|44.34|155916|2761|2462
|853|pear -k --min-overlap 10|42|351340|2857009|44.34|134873|2756|2461
|853|pear -k --min-overlap 15|42|351340|2857330|44.34|134873|2757|2461
|853|pear -k --min-overlap 20|40|351340|2858068|44.34|138191|2759|2462
|853|pear -k --min-overlap 25|41|444200|2859392|44.35|155912|2760|2462
|853|pear -k --min-overlap 30|39|444200|2859691|44.34|155916|2761|2462
|854<sup>**a**</sup>|none|52|179153|2336491|34.99|124556|2199|1986
|854|flash -M 300 --min-overlap=10|50|179153|2331242|34.96|124556|2198|1986
|854|flash -M 300 --min-overlap=15|50|179153|2331251|34.96|124556|2198|1986
|854|flash -M 300 --min-overlap=20|50|179153|2330809|34.96|124556|2196|1985
|854|flash -M 300 --min-overlap=25|50|179153|2331826|34.97|124556|2198|1985
|854|flash -M 300 --min-overlap=30|50|179153|2331826|34.97|124556|2197|1985
|854|pear -k --min-overlap 10|50|179153|2331382|34.97|124556|2198|1986
|854|pear -k --min-overlap 15|51|179153|2332238|34.97|124556|2199|1985
|854|pear -k --min-overlap 20|51|179153|2332238|34.97|124556|2199|1985
|854|pear -k --min-overlap 25|50|179153|2332391|34.97|124556|2200|1985
|854|pear -k --min-overlap 30|50|179153|2332391|34.97|124556|2200|1985
|933<sup>**a**</sup>|none|7|1260240|2444868|36.48|1260240|2351|2059
|933|flash -M 300 --min-overlap=10|8|1260240|2444805|36.48|1260240|2348|2058
|933|flash -M 300 --min-overlap=15|7|1260240|2444844|36.48|1260240|2348|2057
|933|flash -M 300 --min-overlap=20|7|1260240|2444844|36.48|1260240|2348|2057
|933|flash -M 300 --min-overlap=25|7|1260240|2444844|36.48|1260240|2348|2057
|933|flash -M 300 --min-overlap=30|7|1260240|2444844|36.48|1260240|2348|2057
|933|pear -k --min-overlap 10|9|1260234|2441908|36.46|1260234|2351|2058
|933|pear -k --min-overlap 15|8|1260234|2441857|36.46|1260234|2350|2057
|933|pear -k --min-overlap 20|8|1260234|2441857|36.46|1260234|2350|2057
|933|pear -k --min-overlap 25|8|1260234|2441857|36.46|1260234|2350|2057
|933|pear -k --min-overlap 30|8|1260234|2441857|36.46|1260234|2350|2057
<sup>**a**</sup> assembly lacked small insert size warning
