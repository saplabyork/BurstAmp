---
title: "Speaking rate effects on burst amplitude"
author: "Speech and Psycholinguistics Lab-York University"
output: 
  html_document:
    keep_md: true
---



## Background

We're primarily concerned with the relationship between speaking rate and the amplitude (BA) of consonant bursts in onset CVs. We're also interested in whether there are differences in how BA is reflected in languages that differ in how phonological voicing is implemented: English (long-lag VOT) and Indian Tamil (short-lag VOT).

### Methods

Participants (English *n*=12; Tamil *n*=10) self-recorded CVs (at each place of articulation with /a/) at 4 different, self-regulated speeds (slow, normal, fast, very fast).

### Measurements

We looked at a few amplitude landmarks in the burst and following vowel: 

Burst

1. **Ahi**--amplitude of the highest component in the burst spectrum above 3kHz (males), 3.5kHz (females)
2. **Max23**--amplitude of the highest component in the burst spectrum in the range of F2/F3 of the following vowel

Vowel

1. **Av**--average amplitude of F1

Difference measures served as dependent variables:
1. **HiDiff**--Av-Ahi
2. **F23Diff**--Av-Max23

And the temporal measurements:
1. v_dur: Vowel duration of the CV
2. VOT: time from onset of the burst to zero crossing of first periodic wave of the vowel

### Vowel duration
The distribution of v_dur was examined and log-transformed to ensure a more normal distribution --> but do I need it?


The density plots:

![](Burst_proj_files/figure-html/VdurDensity-1.png)<!-- -->
An the log(v_dur) density plot:

![](Burst_proj_files/figure-html/LogVdurDensity-1.png)<!-- -->

### **Note on speaking rate and vowel duration**
The predictions laid out in the introduction rely on there being a clear relationship between speaking rate and vowel duration. That is, it need not be the case that the more syllables a speaker speaks in a given time affect the duration of the syllabic nucleus. Increases in rate may simply result from a decrease in pauses between syllables. Given this complication we might appeal to the term "articulation rate"(Jacewicz, et al. 2009[LVC]), which captures the rate of speech production not including pauses between syllables. The impressionistic self-assessment of articulation rate as "slow," "normal," "fast," and "very fast," leads to a highly variable productions between speakers. In order to avoid bleaching the variation in articulation rate production (which inevitably occurs in designs that aggregate tokens according to impressionistic rate) a continuous measure such as vowel duration (in CVs) is desirable. While it need not be the case that vowels in CVs decrease in duration with increased rate, it remains an empirical question in the present data whether such a relationship is borne out. 

Vowel duration data, which was log transformed to reflect a normal distribution, was modeled as a function of Rate and Language.
Getting data and fixing some factors:


The model:

```
## Linear mixed-effects model fit by REML
##   Data: rate 
##         AIC       BIC   logLik
##   -14009.39 -13890.88 7023.697
## 
## Random effects:
##  Formula: ~1 + rate | sub
##  Structure: General positive-definite, Log-Cholesky parametrization
##               StdDev     Corr                
## (Intercept)   0.06343665 (Intr) rtnrml ratfst
## ratenormal    0.04699030 -0.670              
## ratefast      0.06875148 -0.762  0.823       
## ratevery fast 0.06861315 -0.850  0.624  0.867
## Residual      0.03612480                     
## 
## Fixed effects:  v_dur ~ rate * lang 
##                               Value  Std.Error   DF    t-value p-value
## (Intercept)              0.31368955 0.01841450 3762  17.034922  0.0000
## ratenormal              -0.11262895 0.01396285 3762  -8.066329  0.0000
## ratefast                -0.17885315 0.01999434 3762  -8.945191  0.0000
## ratevery fast           -0.22730680 0.01995739 3762 -11.389606  0.0000
## langTamil               -0.03388071 0.02814385   19  -1.203841  0.2434
## ratenormal:langTamil     0.08765063 0.02121950 3762   4.130665  0.0000
## ratefast:langTamil       0.08573001 0.03056328 3762   2.805000  0.0051
## ratevery fast:langTamil  0.06977217 0.03050288 3762   2.287396  0.0222
##  Correlation: 
##                         (Intr) rtnrml ratfst rtvryf lngTml rtnr:T rtfs:T
## ratenormal              -0.662                                          
## ratefast                -0.763  0.807                                   
## ratevery fast           -0.849  0.615  0.863                            
## langTamil               -0.654  0.433  0.499  0.555                     
## ratenormal:langTamil     0.435 -0.658 -0.531 -0.405 -0.666              
## ratefast:langTamil       0.499 -0.528 -0.654 -0.565 -0.763  0.812       
## ratevery fast:langTamil  0.555 -0.403 -0.565 -0.654 -0.849  0.619  0.863
## 
## Standardized Within-Group Residuals:
##         Min          Q1         Med          Q3         Max 
## -9.50656601 -0.52674499 -0.05010961  0.48470575  5.81683675 
## 
## Number of Observations: 3789
## Number of Groups: 21
```

```
## NOTE: Results may be misleading due to involvement in interactions
```

```
##  contrast           estimate      SE   df t.ratio p.value
##  slow - normal        0.0688 0.01061 3762   6.485  <.0001
##  slow - fast          0.1360 0.01528 3762   8.899  <.0001
##  slow - very fast     0.1924 0.01525 3762  12.617  <.0001
##  normal - fast        0.0672 0.00910 3762   7.386  <.0001
##  normal - very fast   0.1236 0.01203 3762  10.275  <.0001
##  fast - very fast     0.0564 0.00798 3762   7.068  <.0001
## 
## Results are averaged over the levels of: lang 
## Degrees-of-freedom method: containment 
## P value adjustment: tukey method for comparing a family of 4 estimates
```

```
##  contrast           effect.size    SE df lower.CL upper.CL
##  slow - normal             1.90 0.294 19     1.29     2.52
##  slow - fast               3.76 0.423 19     2.88     4.65
##  slow - very fast          5.33 0.422 19     4.44     6.21
##  normal - fast             1.86 0.252 19     1.33     2.39
##  normal - very fast        3.42 0.333 19     2.72     4.12
##  fast - very fast          1.56 0.221 19     1.10     2.02
## 
## Results are averaged over the levels of: lang 
## sigma used for effect sizes: 0.03612 
## Degrees-of-freedom method: inherited from containment when re-gridding 
## Confidence level used: 0.95
```
The plot:

```
## Learn more about sjPlot with 'browseVignettes("sjPlot")'.
```

![](Burst_proj_files/figure-html/model_dur_speed-1.png)<!-- -->

Here is the real data:

```
## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.1 ──
```

```
## ✓ tibble  3.1.6     ✓ dplyr   1.0.7
## ✓ tidyr   1.1.4     ✓ stringr 1.4.0
## ✓ readr   1.4.0     ✓ forcats 0.5.1
## ✓ purrr   0.3.4
```

```
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## x dplyr::collapse() masks nlme::collapse()
## x dplyr::filter()   masks stats::filter()
## x dplyr::lag()      masks stats::lag()
```

```
## 
## The downloaded binary packages are in
## 	/var/folders/nv/72l7lgjs2s5d2y6bbl5wz6w40000gn/T//Rtmpc6da15/downloaded_packages
```

```
## Warning: Ignoring unknown parameters: notch, outlier.shape
```

![](Burst_proj_files/figure-html/Figure2-1.png)<!-- -->

### Make a full data frame for Burst models

The data were coded separately by language. We want to make a full model, so need to combine the dataframes.First clean up the Tamil data: 


Now do something similar for English:


Make a new full data frame:


## Models and Plots
First we need to install "sjPlot" which will give linear model prediction plots with confidence intervals


Make a "lang" column in the **full** data frame. Make new column (log_vdur) because we're taking log of duration measures (as suggested by a reviewer).


### **Models and Plots of F23Diff and HiDiff (with both languages)**
## F23Diff

```
## Linear mixed-effects model fit by REML
##   Data: full 
##        AIC     BIC logLik
##   25684.01 25733.3 -12834
## 
## Random effects:
##  Formula: ~1 + v_dur | sub
##  Structure: General positive-definite, Log-Cholesky parametrization
##             StdDev   Corr  
## (Intercept) 11.33573 (Intr)
## v_dur       29.44814 -0.852
## Residual     9.22694       
## 
## Fixed effects:  F23Diff ~ v_dur * lang 
##                     Value Std.Error   DF   t-value p-value
## (Intercept)      32.47985  3.308899 3484  9.815907  0.0000
## v_dur           -33.81550  8.880011 3484 -3.808048  0.0001
## langTamil         4.96087  4.961482   20  0.999876  0.3293
## v_dur:langTamil   2.36633 13.474675 3484  0.175613  0.8606
##  Correlation: 
##                 (Intr) v_dur  lngTml
## v_dur           -0.844              
## langTamil       -0.667  0.563       
## v_dur:langTamil  0.556 -0.659 -0.848
## 
## Standardized Within-Group Residuals:
##         Min          Q1         Med          Q3         Max 
## -3.18367803 -0.67922280  0.02211743  0.60757542  4.33479943 
## 
## Number of Observations: 3508
## Number of Groups: 22
```
And the F23Diff plot for the full data set:

```
## Scale for 'y' is already present. Adding another scale for 'y', which will
## replace the existing scale.
```

![](Burst_proj_files/figure-html/unnamed-chunk-10-1.png)<!-- -->

The plot confirms the model results: There is no significant language effect, though Tamil is overall 4.5dB higher (more amplitude difference between BA and V; quieter) in the F2/F3 range than English. The effect of logv_dur is evident (negative, decreasing by 6dB per unit of logv_dur). There is no interaction.

## HiDiff

```
## Linear mixed-effects model fit by REML
##   Data: full 
##        AIC      BIC    logLik
##   25966.93 26016.22 -12975.47
## 
## Random effects:
##  Formula: ~1 + v_dur | sub
##  Structure: General positive-definite, Log-Cholesky parametrization
##             StdDev    Corr  
## (Intercept)  9.979220 (Intr)
## v_dur       22.984381 -0.769
## Residual     9.618931       
## 
## Fixed effects:  HiDiff ~ v_dur * lang 
##                     Value Std.Error   DF   t-value p-value
## (Intercept)      36.70851  2.925353 3484 12.548405  0.0000
## v_dur           -29.26607  7.145544 3484 -4.095709  0.0000
## langTamil         6.92498  4.395749   20  1.575382  0.1309
## v_dur:langTamil   9.28543 10.944967 3484  0.848374  0.3963
##  Correlation: 
##                 (Intr) v_dur  lngTml
## v_dur           -0.759              
## langTamil       -0.665  0.505       
## v_dur:langTamil  0.495 -0.653 -0.767
## 
## Standardized Within-Group Residuals:
##        Min         Q1        Med         Q3        Max 
## -3.4845341 -0.6816433 -0.0426431  0.6203153  4.4362520 
## 
## Number of Observations: 3508
## Number of Groups: 22
```

```
## Scale for 'y' is already present. Adding another scale for 'y', which will
## replace the existing scale.
## Scale for 'y' is already present. Adding another scale for 'y', which will
## replace the existing scale.
```

```
## Warning: Removed 1 rows containing missing values (geom_point).
```

![](Burst_proj_files/figure-html/unnamed-chunk-11-1.png)<!-- -->

The plot confirms that HiDiff is higher (lower BA) in Tamil (11.69dB) than English. The effect of logv_dur on HiDiff is the same in both languages (-4.83dB/unit logv_dur).

Now let's make a new FULL data frame with just p-s and k-s (both are in English and Tamil) [Not executed here]

```
full_pk <- full[which(full$POA=="1" | full$POA=="3"),]
```

We're going to model the difference between p and k as a function of vowel duration in the two languages

```
pk_model <- lme(HiDiff ~ POA * v_dur * lang, full_pk, random = ~1 + v_dur | sub)
summary(pk_model)
plot_model(pk_model, type="pred", terms = c("v_dur","POA", "lang"))
```

## Language-specific models

Next we model F23Diff and HiDiff in each language to examine the effects of place of articulation (POA) as well as speaking rate (v_dur).

## **English**

### F23Diff Model

```
## Linear mixed-effects model fit by REML
##   Data: eng 
##        AIC      BIC    logLik
##   13257.21 13313.44 -6618.605
## 
## Random effects:
##  Formula: ~1 + v_dur | sub
##  Structure: General positive-definite, Log-Cholesky parametrization
##             StdDev   Corr  
## (Intercept) 4.903567 (Intr)
## v_dur       6.402900 -0.465
## Residual    6.040665       
## 
## Fixed effects:  F23Diff ~ POA * v_dur 
##                 Value Std.Error   DF    t-value p-value
## (Intercept)  40.03336 1.4815356 2033  27.021534       0
## POAt        -11.18154 0.5975691 2033 -18.711710       0
## POAk        -16.59887 0.6243584 2033 -26.585477       0
## v_dur       -45.39184 2.9717268 2033 -15.274568       0
## POAt:v_dur   31.58582 3.1280450 2033  10.097623       0
## POAk:v_dur   21.97156 3.1549706 2033   6.964109       0
##  Correlation: 
##            (Intr) POAt   POAk   v_dur  POAt:_
## POAt       -0.178                            
## POAk       -0.174  0.446                     
## v_dur      -0.473  0.395  0.383              
## POAt:v_dur  0.154 -0.842 -0.383 -0.488       
## POAk:v_dur  0.156 -0.394 -0.846 -0.490  0.480
## 
## Standardized Within-Group Residuals:
##        Min         Q1        Med         Q3        Max 
## -4.0199691 -0.6695422 -0.0187085  0.6458707  4.1520865 
## 
## Number of Observations: 2050
## Number of Groups: 12
```

### F23Diff Plot

```
## Scale for 'y' is already present. Adding another scale for 'y', which will
## replace the existing scale.
```

![](Burst_proj_files/figure-html/unnamed-chunk-13-1.png)<!-- -->

### HiDiff Model

```
## Linear mixed-effects model fit by REML
##   Data: eng 
##        AIC      BIC   logLik
##   13322.04 13378.27 -6651.02
## 
## Random effects:
##  Formula: ~1 + v_dur | sub
##  Structure: General positive-definite, Log-Cholesky parametrization
##             StdDev    Corr  
## (Intercept)  4.426365 (Intr)
## v_dur       16.305977 -0.423
## Residual     6.118017       
## 
## Fixed effects:  HiDiff ~ POA * v_dur 
##                 Value Std.Error   DF   t-value p-value
## (Intercept)  46.92921  1.354687 2033  34.64212       0
## POAt        -22.87898  0.605698 2033 -37.77292       0
## POAk        -12.43554  0.633669 2033 -19.62465       0
## v_dur       -52.32957  5.299309 2033  -9.87479       0
## POAt:v_dur   51.46151  3.175035 2033  16.20817       0
## POAk:v_dur   33.82137  3.205787 2033  10.55010       0
##  Correlation: 
##            (Intr) POAt   POAk   v_dur  POAt:_
## POAt       -0.197                            
## POAk       -0.193  0.446                     
## v_dur      -0.484  0.225  0.218              
## POAt:v_dur  0.171 -0.841 -0.383 -0.278       
## POAk:v_dur  0.174 -0.394 -0.846 -0.279  0.480
## 
## Standardized Within-Group Residuals:
##         Min          Q1         Med          Q3         Max 
## -3.91696417 -0.64781550 -0.01102455  0.61392322  3.74446300 
## 
## Number of Observations: 2050
## Number of Groups: 12
```

### HiDiff Plot

```
## Scale for 'y' is already present. Adding another scale for 'y', which will
## replace the existing scale.
```

![](Burst_proj_files/figure-html/unnamed-chunk-15-1.png)<!-- -->

## **Tamil**

### F23Diff Model (Tamil)

```
## Linear mixed-effects model fit by REML
##   Data: tam 
##        AIC      BIC    logLik
##   10017.62 10080.98 -4996.812
## 
## Random effects:
##  Formula: ~1 + v_dur | sub
##  Structure: General positive-definite, Log-Cholesky parametrization
##             StdDev    Corr  
## (Intercept) 10.454321 (Intr)
## v_dur       26.695914 -0.665
## Residual     7.351232       
## 
## Fixed effects:  F23Diff ~ POA * v_dur 
##                 Value Std.Error   DF    t-value p-value
## (Intercept)  46.86973  3.471011 1441  13.503194  0.0000
## POAt̪         -5.73475  1.326886 1441  -4.321961  0.0000
## POAʈ        -16.12980  1.405962 1441 -11.472428  0.0000
## POAk        -21.54914  1.386068 1441 -15.546963  0.0000
## v_dur       -23.00645  9.734671 1441  -2.363352  0.0182
## POAt̪:v_dur   -9.93092  6.132161 1441  -1.619481  0.1056
## POAʈ:v_dur    1.11862  6.482267 1441   0.172566  0.8630
## POAk:v_dur    5.60027  6.349590 1441   0.881989  0.3779
##  Correlation:
```

```
## Warning in abbreviate(colnames(x), minlength = rdig + 3): abbreviate used with
## non-ASCII chars
```

```
##            (Intr) POAt̪   POAʈ   POAk   v_dur  POA̪:_  POAʈ:_
## POAt̪       -0.168                                          
## POAʈ       -0.174  0.428                                   
## POAk       -0.165  0.442  0.421                            
## v_dur      -0.689  0.251  0.261  0.248                     
## POAt̪:v_dur  0.153 -0.911 -0.387 -0.401 -0.283              
## POAʈ:v_dur  0.157 -0.389 -0.919 -0.384 -0.290  0.435       
## POAk:v_dur  0.156 -0.403 -0.384 -0.915 -0.289  0.451  0.433
## 
## Standardized Within-Group Residuals:
##         Min          Q1         Med          Q3         Max 
## -3.41911762 -0.61877135 -0.04565378  0.58415200  4.10548712 
## 
## Number of Observations: 1458
## Number of Groups: 10
```

### F23Diff Plot (Tamil)

```
## Scale for 'y' is already present. Adding another scale for 'y', which will
## replace the existing scale.
```

![](Burst_proj_files/figure-html/unnamed-chunk-17-1.png)<!-- -->

#### Pairwise comparisons between POAs (Tamil F23Diff)
First make a model that doesn't have logv_dur as an interaction factor but as an additive factor.


```
##  contrast  estimate    SE   df t.ratio p.value
##   p - t̪        7.72 0.549 1444  14.057  <.0001
##   p - ʈ       15.90 0.554 1444  28.686  <.0001
##   p - k       20.40 0.559 1444  36.472  <.0001
##   t̪ - ʈ        8.18 0.549 1444  14.905  <.0001
##   t̪ - k       12.68 0.552 1444  22.986  <.0001
##   ʈ - k        4.50 0.551 1444   8.164  <.0001
## 
## Degrees-of-freedom method: containment 
## P value adjustment: tukey method for comparing a family of 4 estimates
```

```
##  contrast  effect.size     SE df lower.CL upper.CL
##   p - t̪          1.049 0.0746  9    0.880    1.217
##   p - ʈ          2.160 0.0753  9    1.990    2.331
##   p - k          2.772 0.0760  9    2.600    2.944
##   t̪ - ʈ          1.112 0.0746  9    0.943    1.280
##   t̪ - k          1.723 0.0750  9    1.553    1.893
##   ʈ - k          0.611 0.0749  9    0.442    0.781
## 
## sigma used for effect sizes: 7.359 
## Degrees-of-freedom method: inherited from containment when re-gridding 
## Confidence level used: 0.95
```

### HiDiff Model

```
## Linear mixed-effects model fit by REML
##   Data: tam 
##        AIC      BIC    logLik
##   10371.78 10435.13 -5173.889
## 
## Random effects:
##  Formula: ~1 + v_dur | sub
##  Structure: General positive-definite, Log-Cholesky parametrization
##             StdDev    Corr  
## (Intercept) 11.177645 (Intr)
## v_dur       32.443593 -0.64 
## Residual     8.304259       
## 
## Fixed effects:  HiDiff ~ POA * v_dur 
##                 Value Std.Error   DF   t-value p-value
## (Intercept)  52.49778  3.733423 1441 14.061567  0.0000
## POAk        -13.16528  1.498941 1441 -8.783055  0.0000
## POAʈ        -13.69433  1.588542 1441 -8.620688  0.0000
## POAt̪        -14.00481  1.565813 1441 -8.944115  0.0000
## v_dur        -8.20676 11.644131 1441 -0.704798  0.4810
## POAk:v_dur    2.61460  6.927433 1441  0.377427  0.7059
## POAʈ:v_dur  -16.56657  7.324132 1441 -2.261916  0.0239
## POAt̪:v_dur   -3.11200  7.173997 1441 -0.433789  0.6645
##  Correlation:
```

```
## Warning in abbreviate(colnames(x), minlength = rdig + 3): abbreviate used with
## non-ASCII chars
```

```
##            (Intr) POAk   POAʈ   POAt̪   v_dur  POAk:_ POAʈ:_
## POAk       -0.177                                          
## POAʈ       -0.183  0.428                                   
## POAt̪       -0.174  0.442  0.421                            
## v_dur      -0.674  0.237  0.247  0.235                     
## POAk:v_dur  0.160 -0.911 -0.387 -0.401 -0.268              
## POAʈ:v_dur  0.165 -0.389 -0.919 -0.384 -0.275  0.435       
## POAt̪:v_dur  0.164 -0.403 -0.383 -0.915 -0.273  0.451  0.433
## 
## Standardized Within-Group Residuals:
##         Min          Q1         Med          Q3         Max 
## -3.61561427 -0.65025021 -0.05316989  0.64364004  3.90771232 
## 
## Number of Observations: 1458
## Number of Groups: 10
```

### HiDiff Plot
![](Burst_proj_files/figure-html/unnamed-chunk-21-1.png)<!-- -->

#### Pairwise comparisons between POAs (Tamil HiDiff)
First make a model that doesn't have logv_dur as an interaction factor but as an additive factor.

```
## Linear mixed-effects model fit by REML
##   Data: tam 
##        AIC      BIC    logLik
##   10389.96 10437.49 -5185.979
## 
## Random effects:
##  Formula: ~1 + v_dur | sub
##  Structure: General positive-definite, Log-Cholesky parametrization
##             StdDev    Corr  
## (Intercept) 11.016023 (Intr)
## v_dur       31.817627 -0.631
## Residual     8.318149       
## 
## Fixed effects:  HiDiff ~ POA + v_dur 
##                 Value Std.Error   DF    t-value p-value
## (Intercept)  53.32755  3.603527 1444  14.798709  0.0000
## POAk        -12.61943  0.620485 1444 -20.338004  0.0000
## POAʈ        -17.03336  0.626514 1444 -27.187509  0.0000
## POAt̪        -14.59660  0.632317 1444 -23.084296  0.0000
## v_dur       -12.46611 10.747978 1444  -1.159856  0.2463
##  Correlation: 
##       (Intr) POAk   POAʈ   POAt̪  
## POAk  -0.081                     
## POAʈ  -0.089  0.505              
## POAt̪  -0.067  0.505  0.510       
## v_dur -0.649 -0.010 -0.005 -0.032
## 
## Standardized Within-Group Residuals:
##         Min          Q1         Med          Q3         Max 
## -3.60193377 -0.63661684 -0.06566598  0.64110940  3.98528697 
## 
## Number of Observations: 1458
## Number of Groups: 10
```
Then the pairwise comparisons:

```
##  contrast estimate    SE   df t.ratio p.value
##  p - k       12.62 0.620 1444  20.338  <.0001
##  p - ʈ       17.03 0.627 1444  27.188  <.0001
##  p - t̪       14.60 0.632 1444  23.084  <.0001
##  k - ʈ        4.41 0.620 1444   7.114  <.0001
##  k - t̪        1.98 0.624 1444   3.170  0.0084
##  ʈ - t̪       -2.44 0.623 1444  -3.912  0.0006
## 
## Degrees-of-freedom method: containment 
## P value adjustment: tukey method for comparing a family of 4 estimates
```

```
##  contrast effect.size     SE df lower.CL upper.CL
##  p - k          1.517 0.0746  9   1.3484    1.686
##  p - ʈ          2.048 0.0753  9   1.8774    2.218
##  p - t̪          1.755 0.0760  9   1.5828    1.927
##  k - ʈ          0.531 0.0746  9   0.3619    0.699
##  k - t̪          0.238 0.0750  9   0.0681    0.407
##  ʈ - t̪         -0.293 0.0749  9  -0.4624   -0.124
## 
## sigma used for effect sizes: 8.318 
## Degrees-of-freedom method: inherited from containment when re-gridding 
## Confidence level used: 0.95
```
