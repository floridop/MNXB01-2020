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

## The homework

Your task is to use bash to accomplish the dataset cleanup.

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





## Score and grades (tentative)

# The total score is 27+4. Each task has an associated score.
# Score < 10: failed, grade 1
# 10 <= Score < 26 : 2(acceptable) or 3(good) based on the overall class rating
# Score 26-28 : perfect, grade 4
# Score 29-30 : outstanding, grade 5 only possible if the student does
#               all E1-9 at maximum points AND the OPTIONAL part E10.

