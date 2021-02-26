# Assignment1
Unix assignment


##Data Inspection

###Attributes of fang_et_al_genotypes

here is my snippet of code used for data inspection


cat fang_et_al_genotypes.txt        # inspect this file
head -n 3 fang_et_al_genotypes.txt  # view the format of the first three lines
tail -n 3 fang_et_al_genotypes.txt  # view the format of the last three lines
wc fang_et_al_genotypes.txt         # the number of lines, words, and bytes
ls -l fang_et_al_genotypes.txt      # Total file size
ls -lh fang_et_al_genotypes.txt     # Total (human) file size
du -h fang_et_al_genotypes.txt      # File size
awk -F "\t" '{print NF; exit}' fang_et_al_genotypes.txt   # Number of columns
grep -v "^#" fang_et_al_genotypes.txt | awk -F "\t" '{print NF; exit}'    # the header is excluded in counting the number of columns
tail -n +6 fang_et_al_genotypes.txt  | awk -F "\t" '{print NF; exit}'     # confirming the number of columsn with headers
file fang_et_al_genotypes.txt                                             # inspect the type file (whether it is ASCII or non-ASCII file)
awk -f transpose.awk fang_et_al_genotypes.txt > transposed_genotypes.txt  # Transposing the file





By inspecting this file I learned that:
point 1
It contains bases (A/T/C/G)
It has 2783 lines, 2744038 words, 11051939 (11M) bytes, 986 columns, and ASCII text with very long lines. transposed_genotypes.txt has 2783 columns.

point 2
point 3
or

point 1
point 2
point 3

###Attributes of snp_position.txt
here is my snippet of code used for data inspection
cat snp_position.txt        # inspect this file
head -n 3 snp_position.txt  # view the first three lines
tail -n 3 snp_position.tx   # view the format of the last three lines
wc snp_position.txt         # the number of lines, words, and bytes
ls -l snp_position.txt      # Total file size
ls -lh snp_position.txt     # Total (human) file size
du -h snp_position.txt      # File size
awk -F "\t" '{print NF; exit}' snp_position.txt   # Number of column
tail -n +6 snp_position.txt  | awk -F "\t" '{print NF; exit}' # confirming the number of columsn with head
file snp_position.txt       # inspect the type file (whether it is ASCII or non-ASCII file)
sort -c -k1,1 snp_position.txt  # check if it was sorted or not
echo $?                         # zero return means already sorted, 1 or more is not sorted.


By inspecting this file I learned that:

point 1
It has different types of columns having different information, including SNP and marker ID's, chromosome, positions and others
This file has 984 lines, 13198 words, 82763 bytes, 15 columns, and ASCII text. This file was not sorted by the SNP-ID.
point 2
point 3
or

point 1
point 2
point 3

##Data Processing

 wc -l snp_position.txt transposed_genotypes.txt # look at the number of lines in each file
     984 snp_position.txt
     986 transposed_genotypes.txt
     
     #sorting by SNP_ID
sort -k1,1V transposed_genotypes.txt > sorted_genotypes.txt # sorted and redirected to sorted_genotypes.txt
sort -c -k1,1V sorted_genotypes.txt  #checking if it was not sorted by SNP_ID (nothing printed to our screen if already sorted)
echo $?                              # (zero return, already sorted)

sort -k1,1V snp_position.txt > sorted_snp.txt
sort -c -k1,1V sorted_snp.txt #checking if it was not sorted by SNP_ID
echo $? (zero return, already sorted)

$join
join -1 1 -2 1 -t $'\t' sorted_snp.txt sorted_genotypes.txt > snp_genotypes.txt
wc -l sorted_snp.txt sorted_genotypes.txt snp_genotypes.txt # Number of lines in the files to see if the join was complete
     984 sorted_snp.txt
     986 sorted_genotypes.txt
     958 snp_genotypes.txt # there is no perfect overlap
grep -v "^#" snp_genotypes.txt | cut -f3 | sort | uniq -c | sort -c #unique feature in the third column (12 chromosomes number 1 to ten , unknown and multiple)
grep -v "^#" snp_genotypes.txt | cut -f3 | sort | uniq -c | sort -n #unique "Position" in the third column

grep -v "^#" snp_genotypes.txt | cut -f 1,3,4 > snp_genotypes_3columns.txt # direct columns 1 (SNP_ID), 3 (chromosome), and 4 (position) to a new file



# separate files for the 10 chromosomes


awk '$3 = 1' snp_genotypes.txt > chromosome1.txt
grep -v "^#" "ZMMIL || ZMMLR || ZMMR" chromosome1.txt | cut -f1,3,4 | sort | uniq -c

###Maize Data

here is my snippet of code used for data processing
grep -v "^#" "ZMMIL || ZMMLR || ZMMR" snp_genotypes.txt | sed 's/<TAB>/?/g' > maize_genotypes.txt # maize genotypes selected and missed values replaced by '?'
 # Chromosome 1 to 10 in increasing order
awk '$3 = 1' maize_genotypes.txt | sort -k1,1V > chromosome1.txt        # chromosome 1 selected and sorted by SNP_ID in increasing order
awk '$3 = 2' maize_genotypes.txt | sort -k1,1V > chromosome2.txt
awk '$3 = 3' maize_genotypes.txt | sort -k1,1V > chromosome3.txt
awk '$3 = 4' maize_genotypes.txt | sort -k1,1V > chromosome4.txt
awk '$3 = 5' maize_genotypes.txt | sort -k1,1V > chromosome5.txt
awk '$3 = 6' maize_genotypes.txt | sort -k1,1V > chromosome6.txt
awk '$3 = 7' maize_genotypes.txt | sort -k1,1V > chromosome7.txt
awk '$3 = 8' maize_genotypes.txt | sort -k1,1V > chromosome8.txt
awk '$3 = 9' maize_genotypes.txt | sort -k1,1V > chromosome9.txt
awk '$3 = 10' maize_genotypes.txt | sort -k1,1V > chromosome10.txt

# Chromosome 1 to 10 in decreasing order 
awk '$3 = 1' maize_genotypes.txt | sort -k1,1V -r > chromosome1_rev.txt  # sorted in decreased order
awk '$3 = 2' maize_genotypes.txt | sort -k1,1V -r > chromosome2_rev.txt
awk '$3 = 3' maize_genotypes.txt | sort -k1,1V -r > chromosome3_rev.txt
awk '$3 = 4' maize_genotypes.txt | sort -k1,1V -r > chromosome4_rev.txt
awk '$3 = 5' maize_genotypes.txt | sort -k1,1V -r > chromosome5_rev.txt
awk '$3 = 6' maize_genotypes.txt | sort -k1,1V -r > chromosome6_rev.txt
awk '$3 = 7' maize_genotypes.txt | sort -k1,1V -r > chromosome7_rev.txt
awk '$3 = 8' maize_genotypes.txt | sort -k1,1V -r > chromosome8_rev.txt
awk '$3 = 9' maize_genotypes.txt | sort -k1,1V -r > chromosome9_rev.txt
awk '$3 = 10' maize_genotypes.txt | sort -k1,1V -r > chromosome10_rev.txt

awk '$3 = "unknown"' maize_genotypes.txt > chromosome_unkown.txt # Uknown chromosome

Here is my brief description of what this code does
From the third column (chromosome), a specific chromosome was taken and sorted either in increasing or a decreasing order (except for the uknown chromosome) and the directed to a new file.

###Teosinte Data
grep -v "^#" "ZMPBA || ZMPIL || ZMPJA" snp_genotypes.txt | sed 's/<TAB>/?/g' > teosinte_genotypes.txt # maize genotypes selected and missed values replaced by '?'

here is my snippet of code used for data processing
 # Chromosome 1 to 10 in increasing order
awk '$3 = 1' teosinte_genotypes.txt | sort -k1,1V > teo_chromosome1.txt        # chromosome 1 selected and sorted by SNP_ID in increasing order
awk '$3 = 2' teosinte_genotypes.txt | sort -k1,1V > teo_chromosome2.txt
awk '$3 = 3' teosinte_genotypes.txt | sort -k1,1V > teo_chromosome3.txt
awk '$3 = 4' teosinte_genotypes.txt | sort -k1,1V > teo_chromosome4.txt
awk '$3 = 5' teosinte_genotypes.txt | sort -k1,1V > teo_chromosome5.txt
awk '$3 = 6' teosinte_genotypes.txt | sort -k1,1V > teo_chromosome6.txt
awk '$3 = 7' teosinte_genotypes.txt | sort -k1,1V > teo_chromosome7.txt
awk '$3 = 8' teosinte_genotypes.txt | sort -k1,1V > teo_chromosome8.txt
awk '$3 = 9' teosinte_genotypes.txt | sort -k1,1V > teo_chromosome9.txt
awk '$3 = 10' teosinte_genotypes.txt | sort -k1,1V > teo_chromosome10.txt

# Chromosome 1 to 10 in decreasing order 
awk '$3 = 1' teosinte_genotypes.txt | sort -k1,1V -r > teo_chromosome1_rev.txt  # sorted in decreased order
awk '$3 = 2' teosinte_genotypes.txt | sort -k1,1V -r > teo_chromosome2_rev.txt
awk '$3 = 3' teosinte_genotypes.txt | sort -k1,1V -r > teo_chromosome3_rev.txt
awk '$3 = 4' teosinte_genotypes.txt | sort -k1,1V -r > teo_chromosome4_rev.txt
awk '$3 = 5' teosinte_genotypes.txt | sort -k1,1V -r > teo_chromosome5_rev.txt
awk '$3 = 6' teosinte_genotypes.txt | sort -k1,1V -r > teo_chromosome6_rev.txt
awk '$3 = 7' teosinte_genotypes.txt | sort -k1,1V -r > teo_chromosome7_rev.txt
awk '$3 = 8' teosinte_genotypes.txt | sort -k1,1V -r > teo_chromosome8_rev.txt
awk '$3 = 9' teosinte_genotypes.txt | sort -k1,1V -r > teo_chromosome9_rev.txt
awk '$3 = 10' teosinte_genotypes.txt | sort -k1,1V -r > teo_chromosome10_rev.txt

awk '$3 = "unknown"' teosinte_genotypes.txt > teo_chromosome_unkown.txt  # Uknown chromosome
 

Here is my brief description of what this code does
From the third column (chromosome), a specific chromosome was taken and sorted either in increasing or a decreasing order (except for the uknown chromosome) and the directed to a new file.
