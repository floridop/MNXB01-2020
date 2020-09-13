--------------------------------------------------------
#     WORK IN PROGRESS. Further details will come.
--------------------------------------------------------
# MNXB01-2020-homework-3
--------------------------------------------------------
### Author: Florido Paganelli florido.paganelli@hep.lu.se
###         Lund University
--------------------------------------------------------

## Overview 

In this exercise you will be asked to

1) Download or copy a dataset from a given location
2) Rework the content of such dataset using a bash script
   and various bash tools
3) Write out the results to screen or files in a specific format

## The problem

You are given a dataset from SMHI that contains data about the
temperatures measured by a weather station in Falsterbo:

</nfs/shared/pp/MNXB01/tutorial3/homework3/data/smhi-opendata_1_52240_20200905_163726.csv>

The data appears to be in CSV format, but presents some
inconsistencies.

You goal is to process this data using C++ and you need
to remove these inconsistencies and prepare the file in
a format that is good for C++, that is notoriously bad in
handling text files.

Looking a the dataset you realize there are three things to do:

- Remove metadata at the beginning of the file and in part of
  the initial lines

- Remove the CSV header

- Turn all the separators ; into plain spaces, as you notice that
the data contained never uses spaces. Space separated values are
easier to process for C++.

The initial dataset is in the file 

```
   data/smhi-opendata_1_52240_20200905_163726.csv
```
Its header looks like this:

```csv
Stationsnamn;Klimatnummer;Mäthöjd (meter över marken)
Falsterbo A;52240;2.0

Parameternamn;Beskrivning;Enhet
Lufttemperatur;momentanvärde, 1 gång/tim;degree celsius

Tidsperiod (fr.o.m);Tidsperiod (t.o.m);Höjd (meter över havet);Latitud (decimalgrader);Longitud (decimalgrader)
2009-07-01 00:00:00;2020-09-01 06:00:00;1.575;55.3837;12.8166

Datum;Tid (UTC);Lufttemperatur;Kvalitet;;Tidsutsnitt:
2009-07-01;06:00:00;19.7;G;;Kvalitetskontrollerade historiska data (utom de senaste 3 mån)
2009-07-01;09:00:00;22.3;G;;Tidsperiod (fr.o.m.) = 2009-07-01 00:00:00 (UTC)
2009-07-01;10:00:00;23.1;Y;;Tidsperiod (t.o.m.) = 2020-06-01 06:00:00 (UTC)
2009-07-01;11:00:00;24.0;Y;;Samplingstid = Ej angivet
2009-07-01;12:00:00;23.9;G;;
2009-07-01;13:00:00;25.0;Y;;Kvalitetskoderna:
2009-07-01;14:00:00;25.4;Y;;Grön (G) = Kontrollerade och godkända värden.
2009-07-01;15:00:00;25.5;G;;Gul (Y) = Misstänkta eller aggregerade värden. Grovt kontrollerade arkivdata och okontrollerade realtidsdata (senaste 2 tim).
2009-07-01;16:00:00;23.9;Y;;
...

```

The final result should look **exactly** like the in file

```
   result/rawdata_smhi-opendata_1_52240_20200905_163726.csv
```

that is, like this:

```csv
2009-07-01 06:00:00 19.7 G 
2009-07-01 09:00:00 22.3 G 
2009-07-01 10:00:00 23.1 Y 
2009-07-01 11:00:00 24.0 Y 
2009-07-01 12:00:00 23.9 G 
2009-07-01 13:00:00 25.0 Y 
2009-07-01 14:00:00 25.4 Y 
2009-07-01 15:00:00 25.5 G 
2009-07-01 16:00:00 23.9 Y 
2009-07-01 17:00:00 23.0 Y 
...
```

## The homework

Your task is to use bash to accomplish the dataset cleanup.

Write a script that takes as input a URL or a path to a file similar
to the one in the examples reported below and produces a clean datafile
ready to be processed by C++.

The code must work with any URL/filename, and not just with the ones 
in the examples, as the file might be in different locations
when the teacher tests your code.

In detail, the script must:

1. Be able to run when launched in these two ways:

```bash
# Dataset is at a network location:
  ./smhicleaner.sh 'https://github.com/floridop/MNXB01-2020/raw/master/floridopag/tutorial3/homework3/data/smhi-opendata_1_52240_20200905_163726.csv'

# Dataset is on a filesystem:
  ./smhicleaner.sh /nfs/shared/pp/MNXB01/tutorial3/homework3/data/smhi-opendata_1_52240_20200905_163726.csv
```

2. Show errors and exit with `exit` status `1` if the input parameter is
   missing or the files cannot be retrieved/copied
   
3. Create the following 4 intermediate files:
- `original_smhi-opendata_1_52240_20200905_163726.csv` : a copy of the original file `smhi-opendata_1_52240_20200905_163726.csv`
- `clean1_smhi-opendata_1_52240_20200905_163726.csv`: a cleanup of the original data file with only the lines after the line that starts with `Datum`
- `clean2_smhi-opendata_1_52240_20200905_163726.csv`: a cleanup of `clean1_smhi-opendata_1_52240_20200905_163726.csv` without the additional metadata at the end of each line
- `rawdata_smhi-opendata_1_52240_20200905_163726.csv`: the final result that should contain only the lines about temperature data as in the example above.

4. The script must show the user what is going on and give good errors 
as in the `result/output_*` files (see "Folder structure" below for 
descriptions of each file).
This is an example of the solution and what the output and generated files should look like:
```bash
[pflorido@atariXL solution]$ ./smhicleaner.sh 'https://github.com/floridop/MNXB01-2020/raw/master/floridopag/tutorial3/homework3/data/smhi-opendata_1_52240_20200905_163726.csv'
Downloading https://github.com/floridop/MNXB01-2020/raw/master/floridopag/tutorial3/homework3/data/smhi-opendata_1_52240_20200905_163726.csv into smhi-opendata_1_52240_20200905_163726.csv
--2020-09-13 16:42:55--  https://github.com/floridop/MNXB01-2020/raw/master/floridopag/tutorial3/homework3/data/smhi-opendata_1_52240_20200905_163726.csv
Resolving github.com (github.com)... 140.82.121.3
Connecting to github.com (github.com)|140.82.121.3|:443... connected.
HTTP request sent, awaiting response... 302 Found
Location: https://raw.githubusercontent.com/floridop/MNXB01-2020/master/floridopag/tutorial3/homework3/data/smhi-opendata_1_52240_20200905_163726.csv [following]
--2020-09-13 16:42:56--  https://raw.githubusercontent.com/floridop/MNXB01-2020/master/floridopag/tutorial3/homework3/data/smhi-opendata_1_52240_20200905_163726.csv
Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 199.232.40.133
Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|199.232.40.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 2536195 (2,4M) [text/plain]
Saving to: ‘original_smhi-opendata_1_52240_20200905_163726.csv’

original_smhi-opendata_1_52240_20200905_163726.csv 100%[================================================================================================================>]   2,42M  10,2MB/s    in 0,2s    

2020-09-13 16:42:57 (10,2 MB/s) - ‘original_smhi-opendata_1_52240_20200905_163726.csv’ saved [2536195/2536195]

Finding the first line containing 'Datum'...
Removing the first 11 lines, result in clean1_smhi-opendata_1_52240_20200905_163726.csv
Selecting only relevant columns, result in clean2_smhi-opendata_1_52240_20200905_163726.csv
Substituting the ; with spaces, result in rawdata_smhi-opendata_1_52240_20200905_163726.csv
Filesizes summary:
   file clean1_smhi-opendata_1_52240_20200905_163726.csv has size: 2535790
   file clean2_smhi-opendata_1_52240_20200905_163726.csv has size: 2535330
   file original_smhi-opendata_1_52240_20200905_163726.csv has size: 2536195
   file rawdata_smhi-opendata_1_52240_20200905_163726.csv has size: 2535330
[pflorido@atariXL solution]$ ls
clean1_smhi-opendata_1_52240_20200905_163726.csv  original_smhi-opendata_1_52240_20200905_163726.csv  smhicleaner.sh
clean2_smhi-opendata_1_52240_20200905_163726.csv  rawdata_smhi-opendata_1_52240_20200905_163726.csv
pflorido@atariXL:~/ownCloud/teaching/programming4science2020/florido/Tutorial3/homework3/solution$ 

```




For your convenience, the homework is guided, for you to get used to
writing some pseudocode.

All the above steps are detailed inside the homework pseudocode file
located in `code/smhicleaner.sh.pseudocode` and divided in separate 
exercises with separate score.


### Prepare for the homework

1. Copy the homework directory to your 
home directory on Iridium:

```bash
cp -ar /nfs/shared/pp/MNXB01/tutorial3/homework3 ~/tutorial3/homework3
```

2. Access the directory where the pseudocode is:

```bash
cd ~/tutorial3/homework3/code
```

3. Rename the pseudocode file:

```bash
mv smhicleaner.sh.pseudocode smhicleaner.sh
```

4. Open the file with geany and read and write the code described in the tasks

```bash
geany  smhicleaner.sh&
```

### How to progress 

The file shmicleaner.sh.pseudocode contains pseudocode written by the
teacher to help you progressing and increasing your knowledge of bash.
It consists of 10 exercises `E1-E10` with a defined task and its 
description, and points that you gain for completing the task correctly.

You are requested to write code where the text says `YOUR_CODE_HERE`

**Delete** the text `YOUR_CODE_HERE` and start writing your own code
according to the exercise request. There is no limit in how much you 
write as long as it fulfils the requirements of the exercise.

You can do the exercises one by one and test the result against the
files in the `result/` folder (see folder structure below)

If you are annoyed by the error messages caused by lines that you did 
not yet edit, use the `#` symbol to comment out lines so that bash will 
ignore them as we've seen in the examples in Tutorial 3.

### Folder structure

the tutorial3/homework3 structure is as follows:

```bash
.
├── README.md # this document
├── code # contains the code you have to edit
│   └── smhicleaner.sh.pseudocode  # the file you have to edit
├── data # contains the original data
│   ├── README.md
│   └── smhi-opendata_1_52240_20200905_163726.csv
└── result # contains examples of the final result and the command output
    ├── clean1_smhi-opendata_1_52240_20200905_163726.csv  # output file result of E7
    ├── clean2_smhi-opendata_1_52240_20200905_163726.csv  # output file result of E8
    ├── original_smhi-opendata_1_52240_20200905_163726.csv  # original file: it matches ../data/smhi-opendata_1_52240_20200905_163726.csv
    ├── output_copying  # output of the script when a file path is passed as parameter
    ├── output_downloading  # output of the script when a URL is passed as parameter
    ├── output_error_no_params # output of the script when no parameter is passed
    ├── output_error_problems_downloading_or_copying # output of the script if the download or the copy fails
    └── rawdata_smhi-opendata_1_52240_20200905_163726.csv # output file result of E9, final result.
```

### Tracking your progress

You can track your progress by comparing the output of your script to 
the files

```
└── result # contains examples of the final result and the command output
    ├── output_error_no_params # output of the script when no parameter is passed
    ├── output_error_problems_downloading_or_copying # output of the script if the download or the copy fails
```

Exercises E1 to E6 generate the output shown above.

Then you can check how much of E7-E10 you achieved by comparing each of 
the intermediate files you generate to

```
└── result # contains examples of the final result and the command output
    ├── clean1_smhi-opendata_1_52240_20200905_163726.csv  # output file result of E7
    ├── clean2_smhi-opendata_1_52240_20200905_163726.csv  # output file result of E8
    ├── original_smhi-opendata_1_52240_20200905_163726.csv  # original file: it matches ../data/smhi-opendata_1_52240_20200905_163726.csv
    └── rawdata_smhi-opendata_1_52240_20200905_163726.csv # output file result of E9, final result.
```

And finally compare the final output of your script to

```
└── result # contains examples of the final result and the command output
    ├── output_copying  # output of the script when a file path is passed as parameter
    ├── output_downloading  # output of the script when a URL is passed as parameter
```

for this purpose you can use a text tool called `diff`
<https://www.geeksforgeeks.org/diff-command-linux-examples/>

Compare `myfile` to `resultfile`:
```bash
diff /path/to/myfile /path/to/resultfile
```

For example, if you're editing `smhicleaner.sh` in the `~/tutorial3/homework3/code` folder,
and you generated the first file `clean1_smhi-opendata_1_52240_20200905_163726.csv` in
the same folder, you can do:

```bash
diff ~/tutorial3/homework3/code/clean1_smhi-opendata_1_52240_20200905_163726.csv ~/tutorial3/homework3/result/clean1_smhi-opendata_1_52240_20200905_163726.csv
```

Or if you want a graphical tool you can use `meld`:
<https://meldmerge.org/>

Compare `myfile` to `resultfile`:
```bash
meld /path/to/myfile /path/to/resultfile
```

### Score and grades (tentative)

The total score is 27+4. Each task has an associated score.
- Score < 10: failed, grade 1
- 10 <= Score < 26 : 2(acceptable) or 3(good) based on the overall class rating
- Score 26-28 : perfect, grade 4
- Score 29-30 : outstanding, grade 5 only possible if the student does all E1-9 at maximum points AND the OPTIONAL part E10.

