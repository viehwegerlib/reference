# working with fasta files

Some useful tips from [here](http://bioinformatics.cvr.ac.uk/blog/short-command-lines-for-manipulation-fastq-and-fasta-sequence-files/).

~~~ check length of a sequence given an accession number

# download data, e.g. from NCBI flu database
# convert multiline fasta to singleline 
awk '!/^>/ { printf "%s", $0; n = "\n" } /^>/ { print n $0; n = "" } END { printf "%s", n }' raw_iva_cds.fa > raw_iva_cds_singleline.fa

# given an accession number of some genome segment, count the nucleotides 
# in its sequence
grep -A1 'JX844146' raw_iva_cds_singleline.fa | tail -n 1 | wc | awk '{print $3-$1}'
~~~

~~~ single line fasta

awk '!/^>/ { printf "%s", $0; n = "\n" } /^>/ { print n $0; n = "" } END { printf "%s", n }' multiline.fa > singleline.fa
~~~

~~~ awk multiple field seperators

awk -F'[/=]' '{print ...}'
~~~

~~~ change fasta header, here from ">gb|AB049153:1-2280" to ">AB049153"

awk -F'[|:]' '/^>/{print ">" $2; next}{print}' < iva_cds_minimal.fa
~~~

