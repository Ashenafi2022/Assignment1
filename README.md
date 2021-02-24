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



By inspecting this file I learned that:
point 1
It contains bases (A/T/C/G)
It has 2783 lines, 2744038 words, 11051939 (11M) bytes, 986 columns

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
ls -l snp_position.txt     # Total file size
ls -lh snp_position.txt     # Total (human) file size
du -h snp_position.txt      # File size
awk -F "\t" '{print NF; exit}' snp_position.txt   # Number of column
tail -n +6 snp_position.txt  | awk -F "\t" '{print NF; exit}' # confirming the number of columsn with heade


By inspecting this file I learned that:

point 1
It has different types of columns having different information, including SNP and marker ID's, chromosome, positions and others
This file has 984 lines, 13198 words, 82763 bytes, and 15 columns
point 2
point 3
or

point 1
point 2
point 3
##Data Processing

###Maize Data

here is my snippet of code used for data processing
Here is my brief description of what this code does

###Teosinte Data

here is my snippet of code used for data processing
Here is my brief description of what this code does
