# LinearPartition: Linear-Time Approximation of RNA Folding Partition Function and Base Pairing Probabilities

This repository contains the C++ source code for the LinearPartition project, the first linear-time partition function and base pair probabilities calculation algorithm/software for RNA secondary structures.

[LinearPartition: linear-time approximation of RNA folding partition function and base-pairing probabilities](https://academic.oup.com/bioinformatics/article/36/Supplement_1/i258/5870487). Bioinformatics, Volume 36, Issue Supplement_1, July 2020, Pages i258–i267. ISMB 2020

He Zhang, Liang Zhang, David Mathews, Liang Huang*

\* corresponding author

Web server: http://linearfold.org/partition


## Dependencies
gcc 4.8.5 or above; 
python2.7

## To Compile
```
make
```

## To Run
LinearPartition can be run with:
```
echo SEQUENCE | ./linearpartition [OPTIONS]

OR

cat SEQ_OR_FASTA_FILE | ./linearpartition [OPTIONS]
```
Both FASTA format and pure-sequence format are supported for input.

OPTIONS:
```
-b BEAM_SIZE
```
The beam size (default 100). Use 0 for infinite beam.
```
-V
```
Switches LinearPartition-C (by default) to LinearPartition-V.
```
--verbose
```
Prints out beamsize, Log Partition Coefficient or free energy of ensemble (-V mode) and runtime information. (default False)
```
--sharpturn
```
Enable sharpturn. (default False)
```
-o FILE_NAME
```
Outputs base pairing probability matrix to a file with user specified name. (default False)
```
-r FILE_NAME
```
Output base pairing probability matrix to a file with user specified name (overwrite if the file exists). (default False)
```
--prefix PREFIX_NAME
```
Outputs base pairing probability matrices to files with user specified prefix. (default False)
```
-p
```
Partition function calculation only. (default False)
```
-c CUTOFF
```
Only output base pair probability larger than user specified threshold between 0 and 1. (DEFAULT=0.0)
```

--dumpforest
```
dump forest (all nodes with inside [and outside] log partition functions but no hyperedges) for downstream tasks such as sampling and accessibility (DEFAULT=None)

```
--mea or -M
```
get MEA structure, (DEFAULT=FALSE)

```
--gamma
```
set MEA gamma, (DEFAULT=3.0)

```
--bpseq
```
output MEA structure(s) in bpseq format instead of dot-bracket format

```
--mea_prefix
```
output MEA structure(s) to file(s) with user specified prefix name

```
--threshknot or -T
```
get ThreshKnot structure, (DEFAULT=FALSE)

```
--threshold
```
set ThreshKnot threshknot, (DEFAULT=0.3)

```
--threshknot_prefix
```
output ThreshKnot structure(s) to file(s) with user specified prefix name




## Example: Run Predict
```
cat testseq | ./linearpartition -V --prefix testseq_output
Free Energy of Ensemble: -1.96 kcal/mol
Outputing base pairing probability matrix to testseq_output_1...
Done!
Free Energy of Ensemble: -9.41 kcal/mol
Outputing base pairing probability matrix to testseq_output_2...
Done!
Free Energy of Ensemble: -7.72 kcal/mol
Outputing base pairing probability matrix to testseq_output_3...
Done!
Free Energy of Ensemble: -9.09 kcal/mol
Outputing base pairing probability matrix to testseq_output_4...
Done!
Free Energy of Ensemble: -13.58 kcal/mol
Outputing base pairing probability matrix to testseq_output_5...
Done!

echo GGGCUCGUAGAUCAGCGGUAGAUCGCUUCCUUCGCAAGGAAGCCCUGGGUUCAAAUCCCAGCGAGUCCACCA | ./linearpartition -o output
Log Partition Coefficient: 15.88268
Outputing base pairing probability matrix to output...
Done!
```

## Example: Run Partition Function Calculation Only
```
echo GGGCUCGUAGAUCAGCGGUAGAUCGCUUCCUUCGCAAGGAAGCCCUGGGUUCAAAUCCCAGCGAGUCCACCA | ./linearpartition -V -p --verbose
beam size: 100
Free Energy of Ensemble: -32.14 kcal/mol
Partition Function Calculation Time: 0.01 seconds.
```

## Example: Run Prediction and Output MEA structure
```
echo GGGCUCGUAGAUCAGCGGUAGAUCGCUUCCUUCGCAAGGAAGCCCUGGGUUCAAAUCCCAGCGAGUCCACCA | ./linearpartition -V -M
Free Energy of Ensemble: -32.14 kcal/mol
GGGCUCGUAGAUCAGCGGUAGAUCGCUUCCUUCGCAAGGAAGCCCUGGGUUCAAAUCCCAGCGAGUCCACCA
(((((((..((((.......))))((((((((...)))))))).(((((.......))))))))))))....
```

## Example: Run Prediction and Output ThreshKnot structure in bpseq format
```
echo GUUGUUAUAGCAUAAGAAGUGCAUUUGUUUUAAGCGUAAAAGAUAUGGGACAACUCCA | ./linearpartition -V -T --threshold 0
Free Energy of Ensemble: -8.74 kcal/mol
GUUGUUAUAGCAUAAGAAGUGCAUUUGUUUUAAGCGUAAAAGAUAUGGGACAACUCCA
1 G 54
2 U 53
3 U 52
4 G 51
5 U 50
6 U 49
7 A 0
8 U 0
9 A 0
10 G 22
11 C 21
12 A 20
13 U 19
14 A 0
15 A 0
16 G 0
17 A 0
18 A 0
19 G 13
20 U 12
21 G 11
22 C 10
23 A 0
24 U 34
25 U 33
26 U 45
27 G 44
28 U 43
29 U 42
30 U 41
31 U 40
32 A 37
33 A 25
34 G 24
35 C 47
36 G 46
37 U 32
38 A 0
39 A 0
40 A 31
41 A 30
42 G 29
43 A 28
44 U 27
45 A 26
46 U 36
47 G 35
48 G 0
49 G 6
50 A 5
51 C 4
52 A 3
53 A 2
54 C 1
55 U 0
56 C 0
57 C 0
58 A 0
```

References
-------------

Liang Zhang, He Zhang, David H Mathews, and Liang Huang\*. Threshknot: Thresholded probknot for improved RNA secondary structure prediction. arXiv preprint arXiv:1912.12796.

\* corresponding author