# Assignment1
Unix assignment

##Data Inspection

###Attributes of fang_et_al_genotypes

Here is my snippet of code used for data inspection

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
 It contains bases (A/T/C/G)
 It has 2783 lines, 2744038 words, 11051939 (11M) bytes, 986 columns, and ASCII text with very long lines. transposed_genotypes.txt has 2783 columns.


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
 It has different types of columns having different information, including SNP and marker ID's, chromosome, positions and others.
 This file has 984 lines, 13198 words, 82763 bytes, 15 columns, and ASCII text. This file was not sorted by the SNP-ID.


##Data Processing

##Data Processing  (FINAL)
### Maize Data
# Subset three maize genotypes from fang_et_el file
grep -v "ZMMIL || ZMMLR || ZMMR" fang_et_al_genotypes.txt > maize_3genotypes.txt


# Transpose maize_3genotypes.txt

awk -f transpose.awk maize_3genotypes.txt > transposed_maize.txt

# sort

sort -k1,1V transposed_maize.txt > sorted_maize_3genotypes.txt
sort -c -k1,1V sorted_maize_3genotypes.txt #checking if it was not sorted by SNP_ID
echo $? (zero return, already sorted)


# join with snip_position

join -1 1 -2 1 -t $'\t' sorted_snp.txt sorted_maize_3genotypes.txt > snp_maize.txt

#exclude 3 top rows 

tail -n +4 snp_maize.txt > snp_maize_headless.txt

# Check the first few columns
grep -v "^#" snp_maize_headless.txt | cut -f1,2,3,4 | head -n 5 #second column is chromosome


# subset by Chromosome in increasing order, missed values replaced by ‘?’

awk '$2 = 1' snp_maize_headless.txt | sort -k1,1V | sed 's/<TAB>/?/g' > maize_chromosome1.txt
awk '$2 = 2' snp_maize_headless.txt | sort -k1,1V | sed 's/<TAB>/?/g' > maize_chromosome2.txt
awk '$2 = 3' snp_maize_headless.txt | sort -k1,1V | sed 's/<TAB>/?/g' > maize_chromosome3.txt
awk '$2 = 4' snp_maize_headless.txt | sort -k1,1V | sed 's/<TAB>/?/g' > maize_chromosome4.txt
awk '$2 = 5' snp_maize_headless.txt | sort -k1,1V | sed 's/<TAB>/?/g' > maize_chromosome5.txt
awk '$2 = 6' snp_maize_headless.txt | sort -k1,1V | sed 's/<TAB>/?/g' > maize_chromosome6.txt
awk '$2 = 7' snp_maize_headless.txt | sort -k1,1V | sed 's/<TAB>/?/g' > maize_chromosome7.txt
awk '$2 = 8' snp_maize_headless.txt | sort -k1,1V | sed 's/<TAB>/?/g' > maize_chromosome8.txt
awk '$2 = 9' snp_maize_headless.txt | sort -k1,1V | sed 's/<TAB>/?/g' > maize_chromosome9.txt
awk '$2 = 10' snp_maize_headless.txt | sort -k1,1V | sed 's/<TAB>/?/g' > maize_chromosome10.txt

# order in decreasing order, missed values replaced by ‘-‘
awk '$2 = 1' snp_maize_headless.txt | sort -k1,1V | sed 's/<TAB>/-/g' > maize_chromosome1R.txt
awk '$2 = 2' snp_maize_headless.txt | sort -k1,1V | sed 's/<TAB>/-/g' > maize_chromosome2R.txt
awk '$2 = 3' snp_maize_headless.txt | sort -k1,1V | sed 's/<TAB>/-/g' > maize_chromosome3R.txt
awk '$2 = 4' snp_maize_headless.txt | sort -k1,1V | sed 's/<TAB>/-/g' > maize_chromosome4R.txt
awk '$2 = 5' snp_maize_headless.txt | sort -k1,1V | sed 's/<TAB>/-/g' > maize_chromosome5R.txt
awk '$2 = 6' snp_maize_headless.txt | sort -k1,1V | sed 's/<TAB>/-/g' > maize_chromosome6R.txt
awk '$2 = 7' snp_maize_headless.txt | sort -k1,1V | sed 's/<TAB>/-/g' > maize_chromosome7R.txt
awk '$2 = 8' snp_maize_headless.txt | sort -k1,1V | sed 's/<TAB>/-/g' > maize_chromosome8R.txt
awk '$2 = 9' snp_maize_headless.txt | sort -k1,1V | sed 's/<TAB>/-/g' > maize_chromosome9R.txt
awk '$2 = 10' snp_maize_headless.txt | sort -k1,1V | sed 's/<TAB>/-/g' > maize_chromosome10R.txt

#Unknown chromosome
awk '$2 = "unknown"' snp_maize_headless.txt > maize_chromosome_unknown.txt # Unknown chromosome

awk '$2 = " multiple"' snp_maize_headless.txt > maize_chromosome_multiple.txt # multiple chromosome
 
# ###Teosinte Data
#  Subset three teosinte genotypes from fang_et_el file
grep -v "ZMMIL || ZMMLR || ZMMR" fang_et_al_genotypes.txt > maize_3genotypes.txt
grep -v "ZMPBA || ZMPIL || ZMPJA" fang_et_al_genotypes.txt > teosinte_3genotypes.txt


# Transpose maize_3genotypes.txt

awk -f transpose.awk teosinte_3genotypes.txt > transposed_teosinte.txt

# sort

sort -k1,1V transposed_teosinte.txt > sorted_teosinte_3genotypes.txt
sort -c -k1,1V sorted_teosinte_3genotypes.txt #checking if it was not sorted by SNP_ID
echo $? (zero return, already sorted)


# join with snip_position

join -1 1 -2 1 -t $'\t' sorted_snp.txt sorted_teosinte_3genotypes.txt > snp_teosinte.txt

#exclude 3 top rows 

tail -n +4 snp_teosinte.txt > snp_teosinte_headless.txt

# Check the first few columns
grep -v "^#" snp_teosinte_headless.txt | cut -f1,2,3,4 | head -n 5 #second column is chromosome


# subset by Chromosome in increasing order, missed values replaced by ‘?’

awk '$2 = 1' snp_teosinte_headless.txt | sort -k1,1V | sed 's/<TAB>/?/g' > teosinte_chromosome1.txt
awk '$2 = 2' snp_teosinte_headless.txt | sort -k1,1V | sed 's/<TAB>/?/g' > teosinte_chromosome2.txt
awk '$2 = 3' snp_teosinte_headless.txt | sort -k1,1V | sed 's/<TAB>/?/g' > teosinte_chromosome3.txt
awk '$2 = 4' snp_teosinte_headless.txt | sort -k1,1V | sed 's/<TAB>/?/g' > teosinte_chromosome4.txt
awk '$2 = 5' snp_teosinte_headless.txt | sort -k1,1V | sed 's/<TAB>/?/g' > teosinte_chromosome5.txt
awk '$2 = 6' snp_teosinte_headless.txt | sort -k1,1V | sed 's/<TAB>/?/g' > teosinte_chromosome6.txt
awk '$2 = 7' snp_teosinte_headless.txt | sort -k1,1V | sed 's/<TAB>/?/g' > teosinte_chromosome7.txt
awk '$2 = 8' snp_teosinte_headless.txt | sort -k1,1V | sed 's/<TAB>/?/g' > teosinte_chromosome8.txt
awk '$2 = 9' snp_teosinte_headless.txt | sort -k1,1V | sed 's/<TAB>/?/g' > teosinte_chromosome9.txt
awk '$2 = 10' snp_teosinte_headless.txt | sort -k1,1V | sed 's/<TAB>/?/g' > teosinte_chromosome10.txt

# order in decreasing order, missed values replaced by ‘-‘
awk '$2 = 1' snp_teosinte_headless.txt | sort -k1,1V | sed 's/<TAB>/-/g' > teosinte_chromosome1R.txt
awk '$2 = 2' snp_teosinte_headless.txt | sort -k1,1V | sed 's/<TAB>/-/g' > teosinte_chromosome2R.txt
awk '$2 = 3' snp_teosinte_headless.txt | sort -k1,1V | sed 's/<TAB>/-/g' > teosinte_chromosome3R.txt
awk '$2 = 4' snp_teosinte_headless.txt | sort -k1,1V | sed 's/<TAB>/-/g' > teosinte_chromosome4R.txt
awk '$2 = 5' snp_teosinte_headless.txt | sort -k1,1V | sed 's/<TAB>/-/g' > teosinte_chromosome5R.txt
awk '$2 = 6' snp_teosinte_headless.txt | sort -k1,1V | sed 's/<TAB>/-/g' > teosinte_chromosome6R.txt
awk '$2 = 7' snp_teosinte_headless.txt | sort -k1,1V | sed 's/<TAB>/-/g' > teosinte_chromosome7R.txt
awk '$2 = 8' snp_teosinte_headless.txt | sort -k1,1V | sed 's/<TAB>/-/g' > teosinte_chromosome8R.txt
awk '$2 = 9' snp_teosinte_headless.txt | sort -k1,1V | sed 's/<TAB>/-/g' > teosinte_chromosome9R.txt
awk '$2 = 10' snp_teosinte_headless.txt | sort -k1,1V | sed 's/<TAB>/-/g' > teosinte_chromosome10R.txt

#Unknown chromosome
awk '$2 = "unknown"' snp_teosinte_headless.txt > teosinte_chromosome_unknown.txt # Unknown chromosome

awk '$2 = " multiple"' snp_teosinte_headless.txt > teosinte_chromosome_multiple.txt # multiple chromosome


Here is my brief description of what this code does
From the second column (chromosome), a specific chromosome was taken and sorted either in increasing or a decreasing order (except for the uknown and multiple chromosome) and the directed to a new file.
