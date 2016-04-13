# MACS-script

##Peak Calling

###File names must be changed

## Broad
macs2 callpeak -t /data/colemcqueen/Ivanov/BAM/downloads/GSM1869154.bam -c /data/colemcqueen/Ivanov/BAM/downloads/GSM1869155_ENSEMBL.bam -g mm --broad -n GSM1869154_Pol2_broad -B

## Narrow

macs2 callpeak -t /data/colemcqueen/Ivanov/BAM/downloads/GSM1869154.bam -c /data/colemcqueen/Ivanov/BAM/downloads/GSM1869155_ENSEMBL.bam -g mm -n GSM1869154_Pol2_narrow -B

cut -f 1,2,3,5 GSM1869154_Pol2_narrow_peaks.narrowPeak > GSM1869154_Pol2_narrow_BW.narrowPeak

### Format output data for conversion to bigWig and viewing in the browser
##### Copy file first incase of accidents
cp -r -v  Peak_file.bdg  Copy_of_Peak_file.bdg
### or
‘Peak_file.bdg’ -> ‘Copy_of_Peak_file.bdg’

## Remove the locations below

sed '/^E/d' GSM1869154_Pol2_narrow_BW.narrowPeak > GSM1869154_Pol2_narrow_BW_E.narrowPeak
sed '/^G/d' GSM1869154_Pol2_narrow_BW_E.narrowPeak > GSM1869154_Pol2_narrow_BW_EG.narrowPeak
sed '/^J/d' GSM1869154_Pol2_narrow_BW_EG.narrowPeak > GSM1869154_Pol2_narrow_BW_EGJ.narrowPeak
sed '/^M/d' GSM1869154_Pol2_narrow_BW_EGJ.narrowPeak > GSM1869154_Pol2_narrow_BW_EGJM.narrowPeak

## Add chr to each chromosome number

sed -e 's/^/chr/' GSM1869154_Pol2_narrow_BW_EGJM.narrowPeak > GSM1869154_Pol2_narrow_BW_EGJM_chr.narrowPeak

## Create bigWig
bedGraphToBigWig GSM1869154_Pol2_narrow_BW_EGJM.narrowPeak /data/ref_chrom_sizes/mm10_ENSEMBL/chrom.sizes GSM1869154_Pol2_narrow.bw
