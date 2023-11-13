
# Kulathinal_labProject
# Take genotype_phenotype_data_fb_2023_01.tsv and filter out all "male-limited" and "female limited" 
awk -F'\t' '$5 ~ /limited/ {print $1 "\t" $2 "\t" $3 "\t" $4 "\t" $5}' genotype_phenotype_data_fb_2023_01.tsv > genotype_phenotype_limited.tsv
# With file filtered for just male and female limited, seperate out fbal 
cut -f2 genotype_phenotype_limited.tsv > limited_fbal.txt
# filter out fbgns using list of fbal
grep -wFf limited_fbal.txt fbaltofbgn.tsv > limited_fbaltofbgn.tsv
cut -f3 limited_fbaltofbgn.tsv > limited_fbgn.txt
grep -wFf limited_fbgn.txt fbgn_fbtr_fbpp_fb_2023_05.tsv > limited_fbpp.tsv
grep -wFf limited_fbpp.tsv 7227.protein.links.v12.0.txt > filtered_ppi_interactions.txt
