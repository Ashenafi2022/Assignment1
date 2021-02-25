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
tail -n +6 fang_et_al_genotypes.txt  | awk -F "\t" '{print NF; exit}' # confirming the number of columsn with headers
file fang_et_al_genotypes.txt       # inspect the type file (whether it is ASCII or non-ASCII file)
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
sort -k1,1V transposed_genotypes.txt > sorted_genotypes.txt
sort -c -k1,1V sorted_genotypes.txt
echo $?

sort -k1,1V snp_position.txt > sorted_snp.txt
sort -c -k1,1V sorted_snp.txt #checking is not sorted by SNP_ID
echo $? (zero return means, already sorrted)

$join
join -1 1 -2 1 -t $'\t' sorted_snp.txt sorted_genotypes.txt > snp_genotypes.txt
wc -l sorted_snp.txt sorted_genotypes.txt snp_genotypes.txt # Number of lines in the files to see if the join was complete
     984 sorted_snp.txt
     986 sorted_genotypes.txt
     958 snp_genotypes.txt # there is no perfect overlap



###Maize Data

here is my snippet of code used for data processing
Here is my brief description of what this code does

###Teosinte Data

here is my snippet of code used for data processing
Here is my brief description of what this code does
