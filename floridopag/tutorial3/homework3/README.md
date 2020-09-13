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
temperatures measured by a weather station in Falsterbo.

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
to the one in the examples reported in this document.
The code must work with any URL/filename, and not just with the ones 
in the examples, as the file might be in different locations
when the teacher tests your code.

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
It consists in 10 exercises E1-E10 with a defined task and its 
description, and points that you gain for completing the task correctly.

You are requested to write code where the text says YOUR_CODE_HERE

Delete the text YOUR_CODE_HERE and start writing your own according to
the exercise request. There is no limit in how much you write as long
as it fulfils the requirements of the exercise.

You can do the exercises one by one and test the result against the
files in the /result folder (see folder structure below)

If you are annoyed by the error messages, use the # symbol to comment
out lines so that bash will ignore them as in the examples in
Tutorial 3.




### Score and grades (tentative)

The total score is 27+4. Each task has an associated score.
- Score < 10: failed, grade 1
- 10 <= Score < 26 : 2(acceptable) or 3(good) based on the overall class rating
- Score 26-28 : perfect, grade 4
- Score 29-30 : outstanding, grade 5 only possible if the student does all E1-9 at maximum points AND the OPTIONAL part E10.

