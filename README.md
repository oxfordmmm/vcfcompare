# vcfcompare
Compare VCFs using illumina [hap.py](https://github.com/Illumina/hap.py) and [Nextflow](https://www.nextflow.io/)

## Install nextflow if not exists
See [Nextflow Documentation](https://www.nextflow.io/docs/latest/getstarted.html)

## Install docker if not exists
See [Docker Documentation](https://docs.docker.com/install/linux/docker-ce/ubuntu/)

## Get hap.py docker image from Docker Hub

```
   docker pull pkrusche/hap.py:v0.3.9
```

## Get code
```
   git clone https://github.com/oxfordfun/vcfcompare
```
## Run Test
```
   nextflow run compare.nf -profile docker
```

### Change default parameter for your own data:

--input tests/input (folder with vcf files to be compared against the truevcf)
--ref tests/tests/ref/NC_000962.fasta (reference used for vcf generation)
--refindex tests/ref/NC_000962.fasta.fai (indexed reference by samtools)
--refvcf tests/ref/snps.vcf (true vcf to compare against)

### Test data 
tests/ref/snps.vcf (a vcf generated by [snippy](https://github.com/tseemann/snippy) as true vcf)
tests/input/snps-test-0.vcf (same as snps.vcf)
tests/input/snps-test-1.vcf (one mutation compare to snps.vcf)
tests/input/snps-test-2.vcf (two mutations compare to snps.vcf)

### Test summary
#### snps-test-0.vcf
|Type|Filter|TRUTH.TOTAL|TRUTH.TP|TRUTH.FN|QUERY.TOTAL|QUERY.FP|QUERY.UNK|FP.gt|METRIC.Recall|METRIC.Precision|METRIC.Frac_NA|METRIC.F1_Score|TRUTH.TOTAL.TiTv_ratio|QUERY.TOTAL.TiTv_ratio|TRUTH.TOTAL.het_hom_ratio|QUERY.TOTAL.het_hom_ratio|
|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
|INDEL|ALL|119|119|0|120|0|0|0|1.0|1.0|0.0|1.0|||0.0|0.0|
|INDEL|PASS|119|119|0|120|0|0|0|1.0|1.0|0.0|1.0|||0.0|0.0|
|SNP|ALL|1321|1321|0|1356|0|0|0|1.0|1.0|0.0|1.0|1.68686868687|1.66404715128|0.0|0.0|
|SNP|PASS|1321|1321|0|1356|0|0|0|1.0|1.0|0.0|1.0|1.68686868687|1.66404715128|0.0|0.0|

#### snps-test-1.vcf

|Type|Filter|TRUTH.TOTAL|TRUTH.TP|TRUTH.FN|QUERY.TOTAL|QUERY.FP|QUERY.UNK|FP.gt|METRIC.Recall|METRIC.Precision|METRIC.Frac_NA|METRIC.F1_Score|TRUTH.TOTAL.TiTv_ratio|QUERY.TOTAL.TiTv_ratio|TRUTH.TOTAL.het_hom_ratio|QUERY.TOTAL.het_hom_ratio
|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
|INDEL|ALL|119|119|0|120|0|0|0|1.0|1.0|0.0|1.0|||0.0|0.0|
|INDEL|PASS|119|119|0|120|0|0|0|1.0|1.0|0.0|1.0|||0.0|0.0|
|SNP|ALL|1321|1320|1|1356|1|0|0|0.999243|0.999263|0.0|0.999253|1.68686868687|1.66404715128|0.0|0.0|
|SNP|PASS|1321|1320|1|1356|1|0|0|0.999243|0.999263|0.0|0.999253|1.68686868687|1.66404715128|0.0|0.0|

#### snps-test-2.vcf
|Type|Filter|TRUTH.TOTAL|TRUTH.TP|TRUTH.FN|QUERY.TOTAL|QUERY.FP|QUERY.UNK|FP.gt|METRIC.Recall|METRIC.Precision|METRIC.Frac_NA|METRIC.F1_Score|TRUTH.TOTAL.TiTv_ratio|QUERY.TOTAL.TiTv_ratio|TRUTH.TOTAL.het_hom_ratio|QUERY.TOTAL.het_hom_ratio
|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
|INDEL|ALL|119|119|0|120|0|0|0|1.0|1.0|0.0|1.0|||0.0|0.0|
|INDEL|PASS|119|119|0|120|0|0|0|1.0|1.0|0.0|1.0|||0.0|0.0|
|SNP|ALL|1321|1319|2|1356|2|0|0|0.998486|0.998525|0.0|0.998506|1.68686868687|1.65882352941|0.0|0.0|
|SNP|PASS|1321|1319|2|1356|2|0|0|0.998486|0.998525|0.0|0.998506|1.68686868687|1.65882352941|0.0|0.0|

