## DV_TableauProject2
========================================================
#### Group member: Anna Mengjie Yu (my3852),  Duy Vu (dhv242),  Syed Naqvi (san724)
In this project, we use the same plastid genome data we used in DV_RProject3. 

The length of a gene determines the number of amino acid this gene encodes. The longer the gene, the more likely or more important function it might have. In the plastid genomes, the gene can be in either forward or reverse direction. We partition the genes by direction, and try to discover the length variation of those genes.

We produced the same crosstabs in both R and Tableau.

*********
Load packages


```r
source("../01 SQL Crosstabs/project5_loadPackage.R", echo = TRUE)
```

```
## 
## > require("ggplot2")
```

```
## Loading required package: ggplot2
```

```
## 
## > require("gplots")
```

```
## Loading required package: gplots
## 
## Attaching package: 'gplots'
## 
## The following object is masked from 'package:stats':
## 
##     lowess
```

```
## 
## > require("grid")
```

```
## Loading required package: grid
```

```
## 
## > require("RCurl")
```

```
## Loading required package: RCurl
## Loading required package: bitops
```

```
## 
## > require("reshape2")
```

```
## Loading required package: reshape2
```

```
## 
## > require("tidyr")
```

```
## Loading required package: tidyr
```

```
## 
## > require("dplyr")
```

```
## Loading required package: dplyr
## 
## Attaching package: 'dplyr'
## 
## The following object is masked from 'package:stats':
## 
##     filter
## 
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

```
## 
## > require("jsonlite")
```

```
## Loading required package: jsonlite
## 
## Attaching package: 'jsonlite'
## 
## The following object is masked from 'package:utils':
## 
##     View
```

*********
**Table 1: Rank**
*********
In this table, we created a new column named LEN_RANK, we partition the genes by DIRECTION(forward and reverse). 


We can see that in forward direction, rpoC2 and rpoB genes are ranked top 1 and top 2, respectively, in terms of length. rpo genes are ribosome proterin genes are important gens in charge of protein synthesis.

In ther reverse direction, rnl rRNA is the longest. rRNA is ribosome RNA responsible for transcription and translation. It plays a critical part in protein synthesis.



```r
source("../01 SQL Crosstabs/ocean_rank.R", echo = TRUE)
```

```
## 
## > ocean_rank <- data.frame(fromJSON(getURL(URLencode(gsub("\n", 
## +     " ", "129.152.144.84:5001/rest/native/?query=\"select direction, length, name,  .... [TRUNCATED] 
## 
## > ocean_rank
##     DIRECTION LENGTH        NAME LEN_RANK
## 1     forward   4362   rpoC2 CDS        1
## 2     forward   4095    rpoB CDS        2
## 3     forward   2886    rnl rRNA        3
## 4     forward   2799    clpC CDS        4
## 5     forward   2628    secA CDS        5
## 6     forward   2259    psaA CDS        6
## 7     forward   2202    psaB CDS        7
## 8     forward   2139   rpoC1 CDS        8
## 9     forward   1494   ycf46 CDS        9
## 10    forward   1479    rns rRNA       10
## 11    forward   1473    rbcL CDS       11
## 12    forward   1407   ycf90 CDS       12
## 13    forward   1368    dnaB CDS       13
## 14    forward   1266    ccs1 CDS       14
## 15    forward   1251    secY CDS       15
## 16    forward   1230    tufA CDS       16
## 17    forward   1083    psbA CDS       17
## 18    forward    999    rpoA CDS       18
## 19    forward    987   ycf89 CDS       19
## 20    forward    978    ccsA CDS       20
## 21    forward    963   ycf39 CDS       21
## 22    forward    924    rbcR CDS       22
## 23    forward    864    cbbX CDS       23
## 24    forward    828    rpl2 CDS       24
## 25    forward    804    thiG CDS       25
## 26    forward    717    rpl5 CDS       26
## 27    forward    699    rps2 CDS       27
## 28    forward    648    petB CDS       28
## 29    forward    645    rpl4 CDS       29
## 30    forward    645    rps3 CDS       29
## 31    forward    624    rpl3 CDS       31
## 32    forward    618    rps4 CDS       32
## 33    forward    558    psaF CDS       33
## 34    forward    537    rpl6 CDS       34
## 35    forward    531    rps5 CDS       35
## 36    forward    483    petD CDS       36
## 37    forward    471    rps7 CDS       37
## 38    forward    447    psaL CDS       38
## 39    forward    420    psaD CDS       39
## 40    forward    420    rbcS CDS       39
## 41    forward    417   rpl13 CDS       41
## 42    forward    411   rpl16 CDS       42
## 43    forward    408   rpl18 CDS       43
## 44    forward    405   ycf35 CDS       44
## 45    forward    405    rps9 CDS       44
## 46    forward    399    rps8 CDS       46
## 47    forward    393   rps11 CDS       47
## 48    forward    384   ycf88 CDS       48
## 49    forward    375   rps12 CDS       49
## 50    forward    372   rps13 CDS       50
## 51    forward    366   rpl14 CDS       51
## 52    forward    348   rpl22 CDS       52
## 53    forward    345   psb28 CDS       53
## 54    forward    324   rps10 CDS       54
## 55    forward    318   rpl21 CDS       55
## 56    forward    315   ycf41 CDS       56
## 57    forward    312    rps6 CDS       57
## 58    forward    309   rps20 CDS       58
## 59    forward    279   rps19 CDS       59
## 60    forward    279   rpl23 CDS       59
## 61    forward    255   rps17 CDS       61
## 62    forward    252   rps16 CDS       62
## 63    forward    252   rpl27 CDS       62
## 64    forward    246    psaC CDS       64
## 65    forward    234   rpl24 CDS       65
## 66    forward    219   rpl31 CDS       66
## 67    forward    210    secG CDS       67
## 68    forward    177   rpl29 CDS       68
## 69    forward    165   rpl32 CDS       69
## 70    forward    147   rpl34 CDS       70
## 71    forward    132    psbN CDS       71
## 72    forward    129    petM CDS       72
## 73    forward    126   rrn5 rRNA       73
## 74    forward    126    psaJ CDS       73
## 75    forward    117    psbI CDS       75
## 76    forward    114   rpl36 CDS       76
## 77    forward    111    psaI CDS       77
## 78    forward    111    psbY CDS       77
## 79    forward    100   ffs ncRNA       79
## 80    forward     90    petN CDS       80
## 81    forward     88 trnS-1 tRNA       81
## 82    forward     87 trnS-2 tRNA       82
## 83    forward     87 trnL-2 tRNA       82
## 84    forward     82 trnL-1 tRNA       84
## 85    forward     82   trnY tRNA       84
## 86    forward     74   trnD tRNA       86
## 87    forward     74  trnfM tRNA       86
## 88    forward     74   trnI tRNA       86
## 89    forward     74 trnR-3 tRNA       86
## 90    forward     74   trnP tRNA       86
## 91    forward     73 trnM-1 tRNA       91
## 92    forward     73        trnA       91
## 93    forward     73   trnH tRNA       91
## 94    forward     73 trnR-2 tRNA       91
## 95    forward     72   trnQ tRNA       95
## 96    forward     72   trnK tRNA       95
## 97    forward     72   trnV tRNA       95
## 98    forward     72   trnT tRNA       95
## 99    forward     72   trnN tRNA       95
## 100   forward     71   trnC tRNA      100
## 101   reverse   2886    rnl rRNA        1
## 102   reverse   2799    clpC CDS        2
## 103   reverse   2628    secA CDS        3
## 104   reverse   1929    ftsH CDS        4
## 105   reverse   1824    dnaK CDS        5
## 106   reverse   1593   groEL CDS        6
## 107   reverse   1530    psbB CDS        7
## 108   reverse   1512    atpA CDS        8
## 109   reverse   1494   ycf46 CDS        9
## 110   reverse   1479    rns rRNA       10
## 111   reverse   1458    sufB CDS       11
## 112   reverse   1425    atpB CDS       12
## 113   reverse   1416    psbC CDS       13
## 114   reverse   1359   ycf45 CDS       14
## 115   reverse   1266    ccs1 CDS       15
## 116   reverse   1083    psbA CDS       16
## 117   reverse   1059    chlI CDS       17
## 118   reverse   1056    psbD CDS       18
## 119   reverse    987   ycf89 CDS       19
## 120   reverse    978    ccsA CDS       20
## 121   reverse    945    petA CDS       21
## 122   reverse    924    rbcR CDS       22
## 123   reverse    756    sufC CDS       23
## 124   reverse    741    tatC CDS       24
## 125   reverse    729    atpI CDS       25
## 126   reverse    693    rpl1 CDS       26
## 127   reverse    636   ycf42 CDS       27
## 128   reverse    564    atpD CDS       28
## 129   reverse    555    ycf3 CDS       29
## 130   reverse    546    ycf4 CDS       30
## 131   reverse    540    atpF CDS       31
## 132   reverse    492    psbV CDS       32
## 133   reverse    471    atpG CDS       33
## 134   reverse    426   rpl11 CDS       34
## 135   reverse    423  orf127 CDS       35
## 136   reverse    405   ycf35 CDS       36
## 137   reverse    402    atpE CDS       37
## 138   reverse    387   rpl12 CDS       38
## 139   reverse    363   rpl19 CDS       39
## 140   reverse    360   rpl20 CDS       40
## 141   reverse    334  ssra tmRNA       41
## 142   reverse    318   rpl21 CDS       42
## 143   reverse    312   ycf66 CDS       43
## 144   reverse    303   rps14 CDS       44
## 145   reverse    255    psbE CDS       45
## 146   reverse    252   rpl27 CDS       46
## 147   reverse    249    atpH CDS       47
## 148   reverse    246    psaC CDS       48
## 149   reverse    219   rps18 CDS       49
## 150   reverse    213    thiS CDS       50
## 151   reverse    201    psbH CDS       51
## 152   reverse    198    psaE CDS       52
## 153   reverse    195   rpl35 CDS       53
## 154   reverse    195   ycf33 CDS       53
## 155   reverse    195   rpl33 CDS       53
## 156   reverse    186    psbZ CDS       56
## 157   reverse    165   rpl32 CDS       57
## 158   reverse    147   rpl34 CDS       58
## 159   reverse    135    psbK CDS       59
## 160   reverse    132    psbF CDS       60
## 161   reverse    126   rrn5 rRNA       61
## 162   reverse    120    psbJ CDS       62
## 163   reverse    117    psbL CDS       63
## 164   reverse    117    psbX CDS       63
## 165   reverse    114    petG CDS       65
## 166   reverse    111    psbY CDS       66
## 167   reverse    105   ycf12 CDS       67
## 168   reverse     99    psbT CDS       68
## 169   reverse     96    petL CDS       69
## 170   reverse     93    psaM CDS       70
## 171   reverse     87 trnL-2 tRNA       71
## 172   reverse     85 trnM-2 tRNA       72
## 173   reverse     82 trnL-1 tRNA       73
## 174   reverse     75  flrn ncRNA       74
## 175   reverse     74   trnI tRNA       75
## 176   reverse     74   trnP tRNA       75
## 177   reverse     73   trnF tRNA       77
## 178   reverse     73 trnR-1 tRNA       77
## 179   reverse     73   trnE tRNA       77
## 180   reverse     73   trnA tRNA       77
## 181   reverse     73   trnW tRNA       77
## 182   reverse     72 trnG-2 tRNA       82
## 183   reverse     72   trnC tRNA       82
## 184   reverse     71   trnC tRNA       84
## 185   reverse     71 trnG-1 tRNA       84
```

*********
**Table 2: Max and Difference**
*********
In Table 2, we created two new columns. One named Max_LEN showing the maximum gene length in each gene direction category. The second column LenDiff showing the difference of gene length compared to the maximum gene length in each directory category.

From this table, we can see that the gene length in forward direction varies much more (maxDiff 4291) than gene length in reverse direction(maxDiff 2815).

```r
source("../01 SQL Crosstabs/ocean_diff.R", echo = TRUE)
```

```
## 
## > ocean_diff <- data.frame(fromJSON(getURL(URLencode(gsub("\n", 
## +     " ", "129.152.144.84:5001/rest/native/?query=\"select direction,length, name, l .... [TRUNCATED] 
## 
## > ocean_diff
##     DIRECTION LENGTH        NAME MAX_LEN LEN_DIFF
## 1     forward   4362   rpoC2 CDS    4362        0
## 2     forward   4095    rpoB CDS    4362      267
## 3     forward   2886    rnl rRNA    4362     1476
## 4     forward   2799    clpC CDS    4362     1563
## 5     forward   2628    secA CDS    4362     1734
## 6     forward   2259    psaA CDS    4362     2103
## 7     forward   2202    psaB CDS    4362     2160
## 8     forward   2139   rpoC1 CDS    4362     2223
## 9     forward   1494   ycf46 CDS    4362     2868
## 10    forward   1479    rns rRNA    4362     2883
## 11    forward   1473    rbcL CDS    4362     2889
## 12    forward   1407   ycf90 CDS    4362     2955
## 13    forward   1368    dnaB CDS    4362     2994
## 14    forward   1266    ccs1 CDS    4362     3096
## 15    forward   1251    secY CDS    4362     3111
## 16    forward   1230    tufA CDS    4362     3132
## 17    forward   1083    psbA CDS    4362     3279
## 18    forward    999    rpoA CDS    4362     3363
## 19    forward    987   ycf89 CDS    4362     3375
## 20    forward    978    ccsA CDS    4362     3384
## 21    forward    963   ycf39 CDS    4362     3399
## 22    forward    924    rbcR CDS    4362     3438
## 23    forward    864    cbbX CDS    4362     3498
## 24    forward    828    rpl2 CDS    4362     3534
## 25    forward    804    thiG CDS    4362     3558
## 26    forward    717    rpl5 CDS    4362     3645
## 27    forward    699    rps2 CDS    4362     3663
## 28    forward    648    petB CDS    4362     3714
## 29    forward    645    rpl4 CDS    4362     3717
## 30    forward    645    rps3 CDS    4362     3717
## 31    forward    624    rpl3 CDS    4362     3738
## 32    forward    618    rps4 CDS    4362     3744
## 33    forward    558    psaF CDS    4362     3804
## 34    forward    537    rpl6 CDS    4362     3825
## 35    forward    531    rps5 CDS    4362     3831
## 36    forward    483    petD CDS    4362     3879
## 37    forward    471    rps7 CDS    4362     3891
## 38    forward    447    psaL CDS    4362     3915
## 39    forward    420    rbcS CDS    4362     3942
## 40    forward    420    psaD CDS    4362     3942
## 41    forward    417   rpl13 CDS    4362     3945
## 42    forward    411   rpl16 CDS    4362     3951
## 43    forward    408   rpl18 CDS    4362     3954
## 44    forward    405    rps9 CDS    4362     3957
## 45    forward    405   ycf35 CDS    4362     3957
## 46    forward    399    rps8 CDS    4362     3963
## 47    forward    393   rps11 CDS    4362     3969
## 48    forward    384   ycf88 CDS    4362     3978
## 49    forward    375   rps12 CDS    4362     3987
## 50    forward    372   rps13 CDS    4362     3990
## 51    forward    366   rpl14 CDS    4362     3996
## 52    forward    348   rpl22 CDS    4362     4014
## 53    forward    345   psb28 CDS    4362     4017
## 54    forward    324   rps10 CDS    4362     4038
## 55    forward    318   rpl21 CDS    4362     4044
## 56    forward    315   ycf41 CDS    4362     4047
## 57    forward    312    rps6 CDS    4362     4050
## 58    forward    309   rps20 CDS    4362     4053
## 59    forward    279   rpl23 CDS    4362     4083
## 60    forward    279   rps19 CDS    4362     4083
## 61    forward    255   rps17 CDS    4362     4107
## 62    forward    252   rpl27 CDS    4362     4110
## 63    forward    252   rps16 CDS    4362     4110
## 64    forward    246    psaC CDS    4362     4116
## 65    forward    234   rpl24 CDS    4362     4128
## 66    forward    219   rpl31 CDS    4362     4143
## 67    forward    210    secG CDS    4362     4152
## 68    forward    177   rpl29 CDS    4362     4185
## 69    forward    165   rpl32 CDS    4362     4197
## 70    forward    147   rpl34 CDS    4362     4215
## 71    forward    132    psbN CDS    4362     4230
## 72    forward    129    petM CDS    4362     4233
## 73    forward    126   rrn5 rRNA    4362     4236
## 74    forward    126    psaJ CDS    4362     4236
## 75    forward    117    psbI CDS    4362     4245
## 76    forward    114   rpl36 CDS    4362     4248
## 77    forward    111    psaI CDS    4362     4251
## 78    forward    111    psbY CDS    4362     4251
## 79    forward    100   ffs ncRNA    4362     4262
## 80    forward     90    petN CDS    4362     4272
## 81    forward     88 trnS-1 tRNA    4362     4274
## 82    forward     87 trnL-2 tRNA    4362     4275
## 83    forward     87 trnS-2 tRNA    4362     4275
## 84    forward     82 trnL-1 tRNA    4362     4280
## 85    forward     82   trnY tRNA    4362     4280
## 86    forward     74   trnD tRNA    4362     4288
## 87    forward     74   trnI tRNA    4362     4288
## 88    forward     74   trnP tRNA    4362     4288
## 89    forward     74 trnR-3 tRNA    4362     4288
## 90    forward     74  trnfM tRNA    4362     4288
## 91    forward     73   trnH tRNA    4362     4289
## 92    forward     73        trnA    4362     4289
## 93    forward     73 trnM-1 tRNA    4362     4289
## 94    forward     73 trnR-2 tRNA    4362     4289
## 95    forward     72   trnT tRNA    4362     4290
## 96    forward     72   trnK tRNA    4362     4290
## 97    forward     72   trnV tRNA    4362     4290
## 98    forward     72   trnN tRNA    4362     4290
## 99    forward     72   trnQ tRNA    4362     4290
## 100   forward     71   trnC tRNA    4362     4291
## 101   reverse   2886    rnl rRNA    2886        0
## 102   reverse   2799    clpC CDS    2886       87
## 103   reverse   2628    secA CDS    2886      258
## 104   reverse   1929    ftsH CDS    2886      957
## 105   reverse   1824    dnaK CDS    2886     1062
## 106   reverse   1593   groEL CDS    2886     1293
## 107   reverse   1530    psbB CDS    2886     1356
## 108   reverse   1512    atpA CDS    2886     1374
## 109   reverse   1494   ycf46 CDS    2886     1392
## 110   reverse   1479    rns rRNA    2886     1407
## 111   reverse   1458    sufB CDS    2886     1428
## 112   reverse   1425    atpB CDS    2886     1461
## 113   reverse   1416    psbC CDS    2886     1470
## 114   reverse   1359   ycf45 CDS    2886     1527
## 115   reverse   1266    ccs1 CDS    2886     1620
## 116   reverse   1083    psbA CDS    2886     1803
## 117   reverse   1059    chlI CDS    2886     1827
## 118   reverse   1056    psbD CDS    2886     1830
## 119   reverse    987   ycf89 CDS    2886     1899
## 120   reverse    978    ccsA CDS    2886     1908
## 121   reverse    945    petA CDS    2886     1941
## 122   reverse    924    rbcR CDS    2886     1962
## 123   reverse    756    sufC CDS    2886     2130
## 124   reverse    741    tatC CDS    2886     2145
## 125   reverse    729    atpI CDS    2886     2157
## 126   reverse    693    rpl1 CDS    2886     2193
## 127   reverse    636   ycf42 CDS    2886     2250
## 128   reverse    564    atpD CDS    2886     2322
## 129   reverse    555    ycf3 CDS    2886     2331
## 130   reverse    546    ycf4 CDS    2886     2340
## 131   reverse    540    atpF CDS    2886     2346
## 132   reverse    492    psbV CDS    2886     2394
## 133   reverse    471    atpG CDS    2886     2415
## 134   reverse    426   rpl11 CDS    2886     2460
## 135   reverse    423  orf127 CDS    2886     2463
## 136   reverse    405   ycf35 CDS    2886     2481
## 137   reverse    402    atpE CDS    2886     2484
## 138   reverse    387   rpl12 CDS    2886     2499
## 139   reverse    363   rpl19 CDS    2886     2523
## 140   reverse    360   rpl20 CDS    2886     2526
## 141   reverse    334  ssra tmRNA    2886     2552
## 142   reverse    318   rpl21 CDS    2886     2568
## 143   reverse    312   ycf66 CDS    2886     2574
## 144   reverse    303   rps14 CDS    2886     2583
## 145   reverse    255    psbE CDS    2886     2631
## 146   reverse    252   rpl27 CDS    2886     2634
## 147   reverse    249    atpH CDS    2886     2637
## 148   reverse    246    psaC CDS    2886     2640
## 149   reverse    219   rps18 CDS    2886     2667
## 150   reverse    213    thiS CDS    2886     2673
## 151   reverse    201    psbH CDS    2886     2685
## 152   reverse    198    psaE CDS    2886     2688
## 153   reverse    195   rpl35 CDS    2886     2691
## 154   reverse    195   rpl33 CDS    2886     2691
## 155   reverse    195   ycf33 CDS    2886     2691
## 156   reverse    186    psbZ CDS    2886     2700
## 157   reverse    165   rpl32 CDS    2886     2721
## 158   reverse    147   rpl34 CDS    2886     2739
## 159   reverse    135    psbK CDS    2886     2751
## 160   reverse    132    psbF CDS    2886     2754
## 161   reverse    126   rrn5 rRNA    2886     2760
## 162   reverse    120    psbJ CDS    2886     2766
## 163   reverse    117    psbX CDS    2886     2769
## 164   reverse    117    psbL CDS    2886     2769
## 165   reverse    114    petG CDS    2886     2772
## 166   reverse    111    psbY CDS    2886     2775
## 167   reverse    105   ycf12 CDS    2886     2781
## 168   reverse     99    psbT CDS    2886     2787
## 169   reverse     96    petL CDS    2886     2790
## 170   reverse     93    psaM CDS    2886     2793
## 171   reverse     87 trnL-2 tRNA    2886     2799
## 172   reverse     85 trnM-2 tRNA    2886     2801
## 173   reverse     82 trnL-1 tRNA    2886     2804
## 174   reverse     75  flrn ncRNA    2886     2811
## 175   reverse     74   trnP tRNA    2886     2812
## 176   reverse     74   trnI tRNA    2886     2812
## 177   reverse     73   trnW tRNA    2886     2813
## 178   reverse     73 trnR-1 tRNA    2886     2813
## 179   reverse     73   trnA tRNA    2886     2813
## 180   reverse     73   trnE tRNA    2886     2813
## 181   reverse     73   trnF tRNA    2886     2813
## 182   reverse     72   trnC tRNA    2886     2814
## 183   reverse     72 trnG-2 tRNA    2886     2814
## 184   reverse     71   trnC tRNA    2886     2815
## 185   reverse     71 trnG-1 tRNA    2886     2815
```

*********
**Table 3: Nth Rank**
*********
In Table 3, we created a new column named NTH_LENGTH, we showed the 5th longest gene length in each direction category. We can see that in the forward direction category, the 5th longest gene length is 2628. While in the reverse direction category, the 5th longest gene length is 1824.


```r
source("../01 SQL Crosstabs/ocean_Nth.R", echo = TRUE)
```

```
## 
## > ocean_Nth <- data.frame(fromJSON(getURL(URLencode(gsub("\n", 
## +     " ", "129.152.144.84:5001/rest/native/?query=\"select direction,length, name, nt .... [TRUNCATED] 
## 
## > ocean_Nth
##     DIRECTION LENGTH        NAME NTH_LENGTH
## 1     forward   4362   rpoC2 CDS       2628
## 2     forward   4095    rpoB CDS       2628
## 3     forward   2886    rnl rRNA       2628
## 4     forward   2799    clpC CDS       2628
## 5     forward   2628    secA CDS       2628
## 6     forward   2259    psaA CDS       2628
## 7     forward   2202    psaB CDS       2628
## 8     forward   2139   rpoC1 CDS       2628
## 9     forward   1494   ycf46 CDS       2628
## 10    forward   1479    rns rRNA       2628
## 11    forward   1473    rbcL CDS       2628
## 12    forward   1407   ycf90 CDS       2628
## 13    forward   1368    dnaB CDS       2628
## 14    forward   1266    ccs1 CDS       2628
## 15    forward   1251    secY CDS       2628
## 16    forward   1230    tufA CDS       2628
## 17    forward   1083    psbA CDS       2628
## 18    forward    999    rpoA CDS       2628
## 19    forward    987   ycf89 CDS       2628
## 20    forward    978    ccsA CDS       2628
## 21    forward    963   ycf39 CDS       2628
## 22    forward    924    rbcR CDS       2628
## 23    forward    864    cbbX CDS       2628
## 24    forward    828    rpl2 CDS       2628
## 25    forward    804    thiG CDS       2628
## 26    forward    717    rpl5 CDS       2628
## 27    forward    699    rps2 CDS       2628
## 28    forward    648    petB CDS       2628
## 29    forward    645    rpl4 CDS       2628
## 30    forward    645    rps3 CDS       2628
## 31    forward    624    rpl3 CDS       2628
## 32    forward    618    rps4 CDS       2628
## 33    forward    558    psaF CDS       2628
## 34    forward    537    rpl6 CDS       2628
## 35    forward    531    rps5 CDS       2628
## 36    forward    483    petD CDS       2628
## 37    forward    471    rps7 CDS       2628
## 38    forward    447    psaL CDS       2628
## 39    forward    420    psaD CDS       2628
## 40    forward    420    rbcS CDS       2628
## 41    forward    417   rpl13 CDS       2628
## 42    forward    411   rpl16 CDS       2628
## 43    forward    408   rpl18 CDS       2628
## 44    forward    405   ycf35 CDS       2628
## 45    forward    405    rps9 CDS       2628
## 46    forward    399    rps8 CDS       2628
## 47    forward    393   rps11 CDS       2628
## 48    forward    384   ycf88 CDS       2628
## 49    forward    375   rps12 CDS       2628
## 50    forward    372   rps13 CDS       2628
## 51    forward    366   rpl14 CDS       2628
## 52    forward    348   rpl22 CDS       2628
## 53    forward    345   psb28 CDS       2628
## 54    forward    324   rps10 CDS       2628
## 55    forward    318   rpl21 CDS       2628
## 56    forward    315   ycf41 CDS       2628
## 57    forward    312    rps6 CDS       2628
## 58    forward    309   rps20 CDS       2628
## 59    forward    279   rps19 CDS       2628
## 60    forward    279   rpl23 CDS       2628
## 61    forward    255   rps17 CDS       2628
## 62    forward    252   rps16 CDS       2628
## 63    forward    252   rpl27 CDS       2628
## 64    forward    246    psaC CDS       2628
## 65    forward    234   rpl24 CDS       2628
## 66    forward    219   rpl31 CDS       2628
## 67    forward    210    secG CDS       2628
## 68    forward    177   rpl29 CDS       2628
## 69    forward    165   rpl32 CDS       2628
## 70    forward    147   rpl34 CDS       2628
## 71    forward    132    psbN CDS       2628
## 72    forward    129    petM CDS       2628
## 73    forward    126   rrn5 rRNA       2628
## 74    forward    126    psaJ CDS       2628
## 75    forward    117    psbI CDS       2628
## 76    forward    114   rpl36 CDS       2628
## 77    forward    111    psaI CDS       2628
## 78    forward    111    psbY CDS       2628
## 79    forward    100   ffs ncRNA       2628
## 80    forward     90    petN CDS       2628
## 81    forward     88 trnS-1 tRNA       2628
## 82    forward     87 trnS-2 tRNA       2628
## 83    forward     87 trnL-2 tRNA       2628
## 84    forward     82 trnL-1 tRNA       2628
## 85    forward     82   trnY tRNA       2628
## 86    forward     74   trnD tRNA       2628
## 87    forward     74  trnfM tRNA       2628
## 88    forward     74   trnI tRNA       2628
## 89    forward     74 trnR-3 tRNA       2628
## 90    forward     74   trnP tRNA       2628
## 91    forward     73 trnM-1 tRNA       2628
## 92    forward     73        trnA       2628
## 93    forward     73   trnH tRNA       2628
## 94    forward     73 trnR-2 tRNA       2628
## 95    forward     72   trnQ tRNA       2628
## 96    forward     72   trnK tRNA       2628
## 97    forward     72   trnV tRNA       2628
## 98    forward     72   trnT tRNA       2628
## 99    forward     72   trnN tRNA       2628
## 100   forward     71   trnC tRNA       2628
## 101   reverse   2886    rnl rRNA       1824
## 102   reverse   2799    clpC CDS       1824
## 103   reverse   2628    secA CDS       1824
## 104   reverse   1929    ftsH CDS       1824
## 105   reverse   1824    dnaK CDS       1824
## 106   reverse   1593   groEL CDS       1824
## 107   reverse   1530    psbB CDS       1824
## 108   reverse   1512    atpA CDS       1824
## 109   reverse   1494   ycf46 CDS       1824
## 110   reverse   1479    rns rRNA       1824
## 111   reverse   1458    sufB CDS       1824
## 112   reverse   1425    atpB CDS       1824
## 113   reverse   1416    psbC CDS       1824
## 114   reverse   1359   ycf45 CDS       1824
## 115   reverse   1266    ccs1 CDS       1824
## 116   reverse   1083    psbA CDS       1824
## 117   reverse   1059    chlI CDS       1824
## 118   reverse   1056    psbD CDS       1824
## 119   reverse    987   ycf89 CDS       1824
## 120   reverse    978    ccsA CDS       1824
## 121   reverse    945    petA CDS       1824
## 122   reverse    924    rbcR CDS       1824
## 123   reverse    756    sufC CDS       1824
## 124   reverse    741    tatC CDS       1824
## 125   reverse    729    atpI CDS       1824
## 126   reverse    693    rpl1 CDS       1824
## 127   reverse    636   ycf42 CDS       1824
## 128   reverse    564    atpD CDS       1824
## 129   reverse    555    ycf3 CDS       1824
## 130   reverse    546    ycf4 CDS       1824
## 131   reverse    540    atpF CDS       1824
## 132   reverse    492    psbV CDS       1824
## 133   reverse    471    atpG CDS       1824
## 134   reverse    426   rpl11 CDS       1824
## 135   reverse    423  orf127 CDS       1824
## 136   reverse    405   ycf35 CDS       1824
## 137   reverse    402    atpE CDS       1824
## 138   reverse    387   rpl12 CDS       1824
## 139   reverse    363   rpl19 CDS       1824
## 140   reverse    360   rpl20 CDS       1824
## 141   reverse    334  ssra tmRNA       1824
## 142   reverse    318   rpl21 CDS       1824
## 143   reverse    312   ycf66 CDS       1824
## 144   reverse    303   rps14 CDS       1824
## 145   reverse    255    psbE CDS       1824
## 146   reverse    252   rpl27 CDS       1824
## 147   reverse    249    atpH CDS       1824
## 148   reverse    246    psaC CDS       1824
## 149   reverse    219   rps18 CDS       1824
## 150   reverse    213    thiS CDS       1824
## 151   reverse    201    psbH CDS       1824
## 152   reverse    198    psaE CDS       1824
## 153   reverse    195   rpl35 CDS       1824
## 154   reverse    195   ycf33 CDS       1824
## 155   reverse    195   rpl33 CDS       1824
## 156   reverse    186    psbZ CDS       1824
## 157   reverse    165   rpl32 CDS       1824
## 158   reverse    147   rpl34 CDS       1824
## 159   reverse    135    psbK CDS       1824
## 160   reverse    132    psbF CDS       1824
## 161   reverse    126   rrn5 rRNA       1824
## 162   reverse    120    psbJ CDS       1824
## 163   reverse    117    psbL CDS       1824
## 164   reverse    117    psbX CDS       1824
## 165   reverse    114    petG CDS       1824
## 166   reverse    111    psbY CDS       1824
## 167   reverse    105   ycf12 CDS       1824
## 168   reverse     99    psbT CDS       1824
## 169   reverse     96    petL CDS       1824
## 170   reverse     93    psaM CDS       1824
## 171   reverse     87 trnL-2 tRNA       1824
## 172   reverse     85 trnM-2 tRNA       1824
## 173   reverse     82 trnL-1 tRNA       1824
## 174   reverse     75  flrn ncRNA       1824
## 175   reverse     74   trnI tRNA       1824
## 176   reverse     74   trnP tRNA       1824
## 177   reverse     73   trnF tRNA       1824
## 178   reverse     73 trnR-1 tRNA       1824
## 179   reverse     73   trnE tRNA       1824
## 180   reverse     73   trnA tRNA       1824
## 181   reverse     73   trnW tRNA       1824
## 182   reverse     72 trnG-2 tRNA       1824
## 183   reverse     72   trnC tRNA       1824
## 184   reverse     71   trnC tRNA       1824
## 185   reverse     71 trnG-1 tRNA       1824
```

*********
**Table 4: Accumulation Distribution**
*********
In this Table, we created a new column named CUME_DIST, which shows the accumulative distribution of each gene in each category. From this table, we can see tRNA (transfer RNA) takes most of the lower cumulative percentage in both forward direction category and reverse category.


```r
source("../01 SQL Crosstabs/ocean_cume.R", echo = TRUE)
```

```
## 
## > ocean_cume <- data.frame(fromJSON(getURL(URLencode(gsub("\n", 
## +     " ", "129.152.144.84:5001/rest/native/?query=\"select direction,length, name, c .... [TRUNCATED] 
## 
## > ocean_cume
##     DIRECTION LENGTH        NAME  CUME_DIST
## 1     forward   4362   rpoC2 CDS 1.00000000
## 2     forward   4095    rpoB CDS 0.99000001
## 3     forward   2886    rnl rRNA 0.98000002
## 4     forward   2799    clpC CDS 0.97000003
## 5     forward   2628    secA CDS 0.95999998
## 6     forward   2259    psaA CDS 0.94999999
## 7     forward   2202    psaB CDS 0.94000000
## 8     forward   2139   rpoC1 CDS 0.93000001
## 9     forward   1494   ycf46 CDS 0.92000002
## 10    forward   1479    rns rRNA 0.91000003
## 11    forward   1473    rbcL CDS 0.89999998
## 12    forward   1407   ycf90 CDS 0.88999999
## 13    forward   1368    dnaB CDS 0.88000000
## 14    forward   1266    ccs1 CDS 0.87000000
## 15    forward   1251    secY CDS 0.86000001
## 16    forward   1230    tufA CDS 0.85000002
## 17    forward   1083    psbA CDS 0.83999997
## 18    forward    999    rpoA CDS 0.82999998
## 19    forward    987   ycf89 CDS 0.81999999
## 20    forward    978    ccsA CDS 0.81000000
## 21    forward    963   ycf39 CDS 0.80000001
## 22    forward    924    rbcR CDS 0.79000002
## 23    forward    864    cbbX CDS 0.77999997
## 24    forward    828    rpl2 CDS 0.76999998
## 25    forward    804    thiG CDS 0.75999999
## 26    forward    717    rpl5 CDS 0.75000000
## 27    forward    699    rps2 CDS 0.74000001
## 28    forward    648    petB CDS 0.73000002
## 29    forward    645    rps3 CDS 0.72000003
## 30    forward    645    rpl4 CDS 0.72000003
## 31    forward    624    rpl3 CDS 0.69999999
## 32    forward    618    rps4 CDS 0.69000000
## 33    forward    558    psaF CDS 0.68000001
## 34    forward    537    rpl6 CDS 0.67000002
## 35    forward    531    rps5 CDS 0.66000003
## 36    forward    483    petD CDS 0.64999998
## 37    forward    471    rps7 CDS 0.63999999
## 38    forward    447    psaL CDS 0.63000000
## 39    forward    420    rbcS CDS 0.62000000
## 40    forward    420    psaD CDS 0.62000000
## 41    forward    417   rpl13 CDS 0.60000002
## 42    forward    411   rpl16 CDS 0.58999997
## 43    forward    408   rpl18 CDS 0.57999998
## 44    forward    405   ycf35 CDS 0.56999999
## 45    forward    405    rps9 CDS 0.56999999
## 46    forward    399    rps8 CDS 0.55000001
## 47    forward    393   rps11 CDS 0.54000002
## 48    forward    384   ycf88 CDS 0.52999997
## 49    forward    375   rps12 CDS 0.51999998
## 50    forward    372   rps13 CDS 0.50999999
## 51    forward    366   rpl14 CDS 0.50000000
## 52    forward    348   rpl22 CDS 0.49000001
## 53    forward    345   psb28 CDS 0.47999999
## 54    forward    324   rps10 CDS 0.47000000
## 55    forward    318   rpl21 CDS 0.46000001
## 56    forward    315   ycf41 CDS 0.44999999
## 57    forward    312    rps6 CDS 0.44000000
## 58    forward    309   rps20 CDS 0.43000001
## 59    forward    279   rpl23 CDS 0.41999999
## 60    forward    279   rps19 CDS 0.41999999
## 61    forward    255   rps17 CDS 0.40000001
## 62    forward    252   rpl27 CDS 0.38999999
## 63    forward    252   rps16 CDS 0.38999999
## 64    forward    246    psaC CDS 0.37000000
## 65    forward    234   rpl24 CDS 0.36000001
## 66    forward    219   rpl31 CDS 0.34999999
## 67    forward    210    secG CDS 0.34000000
## 68    forward    177   rpl29 CDS 0.33000001
## 69    forward    165   rpl32 CDS 0.31999999
## 70    forward    147   rpl34 CDS 0.31000000
## 71    forward    132    psbN CDS 0.30000001
## 72    forward    129    petM CDS 0.28999999
## 73    forward    126   rrn5 rRNA 0.28000000
## 74    forward    126    psaJ CDS 0.28000000
## 75    forward    117    psbI CDS 0.25999999
## 76    forward    114   rpl36 CDS 0.25000000
## 77    forward    111    psaI CDS 0.23999999
## 78    forward    111    psbY CDS 0.23999999
## 79    forward    100   ffs ncRNA 0.22000000
## 80    forward     90    petN CDS 0.20999999
## 81    forward     88 trnS-1 tRNA 0.20000000
## 82    forward     87 trnL-2 tRNA 0.19000000
## 83    forward     87 trnS-2 tRNA 0.19000000
## 84    forward     82 trnL-1 tRNA 0.17000000
## 85    forward     82   trnY tRNA 0.17000000
## 86    forward     74   trnD tRNA 0.15000001
## 87    forward     74   trnI tRNA 0.15000001
## 88    forward     74   trnP tRNA 0.15000001
## 89    forward     74 trnR-3 tRNA 0.15000001
## 90    forward     74  trnfM tRNA 0.15000001
## 91    forward     73   trnH tRNA 0.10000000
## 92    forward     73        trnA 0.10000000
## 93    forward     73 trnM-1 tRNA 0.10000000
## 94    forward     73 trnR-2 tRNA 0.10000000
## 95    forward     72   trnT tRNA 0.06000000
## 96    forward     72   trnK tRNA 0.06000000
## 97    forward     72   trnV tRNA 0.06000000
## 98    forward     72   trnN tRNA 0.06000000
## 99    forward     72   trnQ tRNA 0.06000000
## 100   forward     71   trnC tRNA 0.01000000
## 101   reverse   2886    rnl rRNA 1.00000000
## 102   reverse   2799    clpC CDS 0.98823529
## 103   reverse   2628    secA CDS 0.97647059
## 104   reverse   1929    ftsH CDS 0.96470588
## 105   reverse   1824    dnaK CDS 0.95294118
## 106   reverse   1593   groEL CDS 0.94117647
## 107   reverse   1530    psbB CDS 0.92941177
## 108   reverse   1512    atpA CDS 0.91764706
## 109   reverse   1494   ycf46 CDS 0.90588236
## 110   reverse   1479    rns rRNA 0.89411765
## 111   reverse   1458    sufB CDS 0.88235295
## 112   reverse   1425    atpB CDS 0.87058824
## 113   reverse   1416    psbC CDS 0.85882354
## 114   reverse   1359   ycf45 CDS 0.84705883
## 115   reverse   1266    ccs1 CDS 0.83529413
## 116   reverse   1083    psbA CDS 0.82352942
## 117   reverse   1059    chlI CDS 0.81176472
## 118   reverse   1056    psbD CDS 0.80000001
## 119   reverse    987   ycf89 CDS 0.78823531
## 120   reverse    978    ccsA CDS 0.77647060
## 121   reverse    945    petA CDS 0.76470590
## 122   reverse    924    rbcR CDS 0.75294119
## 123   reverse    756    sufC CDS 0.74117649
## 124   reverse    741    tatC CDS 0.72941178
## 125   reverse    729    atpI CDS 0.71764708
## 126   reverse    693    rpl1 CDS 0.70588237
## 127   reverse    636   ycf42 CDS 0.69411767
## 128   reverse    564    atpD CDS 0.68235296
## 129   reverse    555    ycf3 CDS 0.67058825
## 130   reverse    546    ycf4 CDS 0.65882355
## 131   reverse    540    atpF CDS 0.64705884
## 132   reverse    492    psbV CDS 0.63529414
## 133   reverse    471    atpG CDS 0.62352943
## 134   reverse    426   rpl11 CDS 0.61176473
## 135   reverse    423  orf127 CDS 0.60000002
## 136   reverse    405   ycf35 CDS 0.58823532
## 137   reverse    402    atpE CDS 0.57647061
## 138   reverse    387   rpl12 CDS 0.56470591
## 139   reverse    363   rpl19 CDS 0.55294120
## 140   reverse    360   rpl20 CDS 0.54117650
## 141   reverse    334  ssra tmRNA 0.52941179
## 142   reverse    318   rpl21 CDS 0.51764709
## 143   reverse    312   ycf66 CDS 0.50588238
## 144   reverse    303   rps14 CDS 0.49411765
## 145   reverse    255    psbE CDS 0.48235294
## 146   reverse    252   rpl27 CDS 0.47058824
## 147   reverse    249    atpH CDS 0.45882353
## 148   reverse    246    psaC CDS 0.44705883
## 149   reverse    219   rps18 CDS 0.43529412
## 150   reverse    213    thiS CDS 0.42352942
## 151   reverse    201    psbH CDS 0.41176471
## 152   reverse    198    psaE CDS 0.40000001
## 153   reverse    195   rpl35 CDS 0.38823530
## 154   reverse    195   ycf33 CDS 0.38823530
## 155   reverse    195   rpl33 CDS 0.38823530
## 156   reverse    186    psbZ CDS 0.35294119
## 157   reverse    165   rpl32 CDS 0.34117648
## 158   reverse    147   rpl34 CDS 0.32941177
## 159   reverse    135    psbK CDS 0.31764707
## 160   reverse    132    psbF CDS 0.30588236
## 161   reverse    126   rrn5 rRNA 0.29411766
## 162   reverse    120    psbJ CDS 0.28235295
## 163   reverse    117    psbX CDS 0.27058825
## 164   reverse    117    psbL CDS 0.27058825
## 165   reverse    114    petG CDS 0.24705882
## 166   reverse    111    psbY CDS 0.23529412
## 167   reverse    105   ycf12 CDS 0.22352941
## 168   reverse     99    psbT CDS 0.21176471
## 169   reverse     96    petL CDS 0.20000000
## 170   reverse     93    psaM CDS 0.18823530
## 171   reverse     87 trnL-2 tRNA 0.17647059
## 172   reverse     85 trnM-2 tRNA 0.16470589
## 173   reverse     82 trnL-1 tRNA 0.15294118
## 174   reverse     75  flrn ncRNA 0.14117648
## 175   reverse     74   trnI tRNA 0.12941177
## 176   reverse     74   trnP tRNA 0.12941177
## 177   reverse     73   trnE tRNA 0.10588235
## 178   reverse     73   trnW tRNA 0.10588235
## 179   reverse     73   trnF tRNA 0.10588235
## 180   reverse     73 trnR-1 tRNA 0.10588235
## 181   reverse     73   trnA tRNA 0.10588235
## 182   reverse     72 trnG-2 tRNA 0.04705882
## 183   reverse     72   trnC tRNA 0.04705882
## 184   reverse     71   trnC tRNA 0.02352941
## 185   reverse     71 trnG-1 tRNA 0.02352941
```

*********
**Tableau** 

**Rank Table**
In this table, we created a new column rank, partition the data by direction, and order by length in descending order. We generated exactly the same table as in R. In addition, we added the rank filter, where the user can select any range of rank they would like to see.

*********
**Difference** 
In the Difference table, we partitioned the data by direction, order by the length of gene in descending order. We generated two new columns MaxLen and Difference Len, showing the difference between the maximum gene length in each category with individual gene.

*********
**Nth** 
In the Nth table, we partioned the data by direction, order by the length of gene in descending order. We generated one new column showing the length of the gene in certain rank. We created a parameter Nth, the user can change the Nth from 1 to 5 to see the nth maximum gene length in each direction category.

*********
**Cume_dist** 
In the Cume_dist table, we caculated the cumulative distribution of gene length in each direction category. And in teh cumeFig, we visualized the distribution of gene length in different direction category. Different genes category are indicated by different color, and the cumulative sum is also represented by the size of the bar.


