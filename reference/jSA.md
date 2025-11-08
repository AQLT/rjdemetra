# Functions around 'jSA' objects

`get_dictionary` returns the indicators that can be extracted from
`"jSA"` objects, `get_indicators` extracts a list of indicators `jSA2R`
returns the corresponding `"SA"`.

## Usage

``` r
get_jspec(x, ...)

get_dictionary(x)

get_indicators(x, ...)

jSA2R(x, userdefined = NULL)
```

## Arguments

- x:

  a `"jSA"` object.

- ...:

  characters containing the names of the indicators to extract.

- userdefined:

  a userdefined vector containing the names of additional output
  variables (see [`user_defined_variables`](user_defined_variables.md)).
  Only used for `"SA"` objects.

## Value

`get_dictionary` returns a vector of characters, `get_indicators`
returns a list containing the indicators that are extracted, `jSA2R`
returns a `"SA"` or a `"regarima"` object and `get_jspec` returns a Java
object.

## Details

A `"jSA"` object is a list of three elements:

- `"result"`: the Java object containing the results of a seasonal
  adjustment or a pre-adjustment method.

- `"spec"`: the Java object containing the specification of a seasonal
  adjustment or a pre-adjustment method.

- `"dictionary"`: the Java object containing the dictionary of a
  seasonal adjustment or a pre-adjustment method. In particular, it
  contains all the user-defined regressors.

`get_dictionary` returns the list of indicators that can be extracted
from a `jSA` object by the function `get_indicators`.

`jSA2R` returns the corresponding formatted seasonally adjusted (`"SA"`
object) or RegARIMA (`"regarima"` object) model.

`get_jspec` returns the Java object that contains the specification of
an object. Such object can be of type `"jSA"`, `"X13"`, `"TRAMO_SEATS"`
or `"sa_item"`.

## Examples

``` r
myseries <- ipi_c_eu[, "FR"]
mysa <- jx13(myseries, spec = "RSA5c")
get_dictionary(mysa)
#>   [1] "y"                                              
#>   [2] "y_f"                                            
#>   [3] "t"                                              
#>   [4] "t_f"                                            
#>   [5] "sa"                                             
#>   [6] "sa_f"                                           
#>   [7] "s"                                              
#>   [8] "s_f"                                            
#>   [9] "i"                                              
#>  [10] "i_f"                                            
#>  [11] "mode"                                           
#>  [12] "preprocessing.model.span.start"                 
#>  [13] "preprocessing.model.span.end"                   
#>  [14] "preprocessing.model.span.n"                     
#>  [15] "preprocessing.model.espan.start"                
#>  [16] "preprocessing.model.espan.end"                  
#>  [17] "preprocessing.model.espan.n"                    
#>  [18] "preprocessing.model.log"                        
#>  [19] "preprocessing.model.adjust"                     
#>  [20] "preprocessing.model.y"                          
#>  [21] "preprocessing.model.y_f"                        
#>  [22] "preprocessing.model.y_ef"                       
#>  [23] "preprocessing.model.yc"                         
#>  [24] "preprocessing.model.yc_f"                       
#>  [25] "preprocessing.model.yc_ef"                      
#>  [26] "preprocessing.model.l"                          
#>  [27] "preprocessing.model.y_lin"                      
#>  [28] "preprocessing.model.y_lin_f"                    
#>  [29] "preprocessing.model.ycal"                       
#>  [30] "preprocessing.model.ycal_f"                     
#>  [31] "preprocessing.model.det"                        
#>  [32] "preprocessing.model.det_f"                      
#>  [33] "preprocessing.model.l_f"                        
#>  [34] "preprocessing.model.l_b"                        
#>  [35] "preprocessing.model.cal"                        
#>  [36] "preprocessing.model.cal_f"                      
#>  [37] "preprocessing.model.tde"                        
#>  [38] "preprocessing.model.tde_f"                      
#>  [39] "preprocessing.model.mhe"                        
#>  [40] "preprocessing.model.mhe_f"                      
#>  [41] "preprocessing.model.ee"                         
#>  [42] "preprocessing.model.ee_f"                       
#>  [43] "preprocessing.model.omhe"                       
#>  [44] "preprocessing.model.omhe_f"                     
#>  [45] "preprocessing.model.out(*)"                     
#>  [46] "preprocessing.model.out_f"                      
#>  [47] "preprocessing.model.out_i"                      
#>  [48] "preprocessing.model.out_i_f"                    
#>  [49] "preprocessing.model.out_t"                      
#>  [50] "preprocessing.model.out_t_f"                    
#>  [51] "preprocessing.model.out_s"                      
#>  [52] "preprocessing.model.out_s_f"                    
#>  [53] "preprocessing.model.reg"                        
#>  [54] "preprocessing.model.reg_f"                      
#>  [55] "preprocessing.model.reg_t"                      
#>  [56] "preprocessing.model.reg_t_f"                    
#>  [57] "preprocessing.model.reg_s"                      
#>  [58] "preprocessing.model.reg_s_f"                    
#>  [59] "preprocessing.model.reg_i"                      
#>  [60] "preprocessing.model.reg_i_f"                    
#>  [61] "preprocessing.model.reg_sa"                     
#>  [62] "preprocessing.model.reg_sa_f"                   
#>  [63] "preprocessing.model.reg_y"                      
#>  [64] "preprocessing.model.reg_y_f"                    
#>  [65] "preprocessing.model.reg_u"                      
#>  [66] "preprocessing.model.reg_u_f"                    
#>  [67] "preprocessing.model.fullresiduals"              
#>  [68] "preprocessing.model.lp"                         
#>  [69] "preprocessing.model.ntd"                        
#>  [70] "preprocessing.model.nmh"                        
#>  [71] "preprocessing.model.td(*)"                      
#>  [72] "preprocessing.model.easter"                     
#>  [73] "preprocessing.model.nout"                       
#>  [74] "preprocessing.model.noutao"                     
#>  [75] "preprocessing.model.noutls"                     
#>  [76] "preprocessing.model.nouttc"                     
#>  [77] "preprocessing.model.noutso"                     
#>  [78] "preprocessing.model.coefficients"               
#>  [79] "preprocessing.model.description"                
#>  [80] "preprocessing.model.covar"                      
#>  [81] "preprocessing.model.pcovar"                     
#>  [82] "preprocessing.model.fcasts(?)"                  
#>  [83] "preprocessing.model.bcasts(?)"                  
#>  [84] "preprocessing.model.lin_fcasts(?)"              
#>  [85] "preprocessing.model.lin_bcasts(?)"              
#>  [86] "preprocessing.model.efcasts(?)"                 
#>  [87] "preprocessing.arima.parameters"                 
#>  [88] "preprocessing.arima.p"                          
#>  [89] "preprocessing.arima.d"                          
#>  [90] "preprocessing.arima.q"                          
#>  [91] "preprocessing.arima.bp"                         
#>  [92] "preprocessing.arima.bd"                         
#>  [93] "preprocessing.arima.bq"                         
#>  [94] "preprocessing.likelihood.neffectiveobs"         
#>  [95] "preprocessing.likelihood.np"                    
#>  [96] "preprocessing.likelihood.logvalue"              
#>  [97] "preprocessing.likelihood.adjustedlogvalue"      
#>  [98] "preprocessing.likelihood.ssqerr"                
#>  [99] "preprocessing.likelihood.aic"                   
#> [100] "preprocessing.likelihood.aicc"                  
#> [101] "preprocessing.likelihood.bic"                   
#> [102] "preprocessing.likelihood.bicc"                  
#> [103] "preprocessing.likelihood.ser"                   
#> [104] "preprocessing.likelihood.ser-ml"                
#> [105] "preprocessing.residuals.res"                    
#> [106] "preprocessing.residuals.mean"                   
#> [107] "preprocessing.residuals.skewness"               
#> [108] "preprocessing.residuals.kurtosis"               
#> [109] "preprocessing.residuals.dh"                     
#> [110] "preprocessing.residuals.lb"                     
#> [111] "preprocessing.residuals.lb2"                    
#> [112] "preprocessing.residuals.seaslb"                 
#> [113] "preprocessing.residuals.bp"                     
#> [114] "preprocessing.residuals.bp2"                    
#> [115] "preprocessing.residuals.seasbp"                 
#> [116] "preprocessing.residuals.nruns"                  
#> [117] "preprocessing.residuals.lruns"                  
#> [118] "mstats.M(*)"                                    
#> [119] "mstats.Q"                                       
#> [120] "mstats.Q-M2"                                    
#> [121] "decomposition.a1"                               
#> [122] "decomposition.a1a"                              
#> [123] "decomposition.a1b"                              
#> [124] "decomposition.a6"                               
#> [125] "decomposition.a7"                               
#> [126] "decomposition.a8"                               
#> [127] "decomposition.a8t"                              
#> [128] "decomposition.a8s"                              
#> [129] "decomposition.a8i"                              
#> [130] "decomposition.a9"                               
#> [131] "decomposition.a9sa"                             
#> [132] "decomposition.a9u"                              
#> [133] "decomposition.a9ser"                            
#> [134] "decomposition.b1"                               
#> [135] "decomposition.b2"                               
#> [136] "decomposition.b3"                               
#> [137] "decomposition.b4"                               
#> [138] "decomposition.b5"                               
#> [139] "decomposition.b6"                               
#> [140] "decomposition.b7"                               
#> [141] "decomposition.b8"                               
#> [142] "decomposition.b9"                               
#> [143] "decomposition.b10"                              
#> [144] "decomposition.b11"                              
#> [145] "decomposition.b12"                              
#> [146] "decomposition.b13"                              
#> [147] "decomposition.b14"                              
#> [148] "decomposition.b15"                              
#> [149] "decomposition.b16"                              
#> [150] "decomposition.b17"                              
#> [151] "decomposition.b18"                              
#> [152] "decomposition.b19"                              
#> [153] "decomposition.b20"                              
#> [154] "decomposition.c1"                               
#> [155] "decomposition.c2"                               
#> [156] "decomposition.c3"                               
#> [157] "decomposition.c4"                               
#> [158] "decomposition.c5"                               
#> [159] "decomposition.c6"                               
#> [160] "decomposition.c7"                               
#> [161] "decomposition.c8"                               
#> [162] "decomposition.c9"                               
#> [163] "decomposition.c10"                              
#> [164] "decomposition.c11"                              
#> [165] "decomposition.c12"                              
#> [166] "decomposition.c13"                              
#> [167] "decomposition.c14"                              
#> [168] "decomposition.c15"                              
#> [169] "decomposition.c16"                              
#> [170] "decomposition.c17"                              
#> [171] "decomposition.c18"                              
#> [172] "decomposition.c19"                              
#> [173] "decomposition.c20"                              
#> [174] "decomposition.d1"                               
#> [175] "decomposition.d2"                               
#> [176] "decomposition.d3"                               
#> [177] "decomposition.d4"                               
#> [178] "decomposition.d5"                               
#> [179] "decomposition.d6"                               
#> [180] "decomposition.d7"                               
#> [181] "decomposition.d8"                               
#> [182] "decomposition.d9"                               
#> [183] "decomposition.d10"                              
#> [184] "decomposition.d10a"                             
#> [185] "decomposition.d10b"                             
#> [186] "decomposition.d11"                              
#> [187] "decomposition.d11a"                             
#> [188] "decomposition.d12"                              
#> [189] "decomposition.d12a"                             
#> [190] "decomposition.d13"                              
#> [191] "decomposition.d14"                              
#> [192] "decomposition.d15"                              
#> [193] "decomposition.d16"                              
#> [194] "decomposition.d16a"                             
#> [195] "decomposition.d16b"                             
#> [196] "decomposition.d18"                              
#> [197] "decomposition.d19"                              
#> [198] "decomposition.d20"                              
#> [199] "decomposition.e1"                               
#> [200] "decomposition.e2"                               
#> [201] "decomposition.e3"                               
#> [202] "decomposition.e11"                              
#> [203] "decomposition.y_cmp"                            
#> [204] "decomposition.t_cmp"                            
#> [205] "decomposition.i_cmp"                            
#> [206] "decomposition.s_cmp"                            
#> [207] "decomposition.sa_cmp"                           
#> [208] "decomposition.y_cmp_f"                          
#> [209] "decomposition.t_cmp_f"                          
#> [210] "decomposition.i_cmp_f"                          
#> [211] "decomposition.s_cmp_f"                          
#> [212] "decomposition.sa_cmp_f"                         
#> [213] "decomposition.d9filter"                         
#> [214] "decomposition.slen"                             
#> [215] "decomposition.d12filter"                        
#> [216] "decomposition.tlen"                             
#> [217] "diagnostics.qs"                                 
#> [218] "diagnostics.ftest"                              
#> [219] "diagnostics.qs.on.i"                            
#> [220] "diagnostics.ftest.on.i"                         
#> [221] "diagnostics.combined.all.kruskalwallis"         
#> [222] "diagnostics.combined.all.stable"                
#> [223] "diagnostics.combined.all.evolutive"             
#> [224] "diagnostics.combined.all.summary"               
#> [225] "diagnostics.combined.all.stable.ssm"            
#> [226] "diagnostics.combined.all.stable.ssr"            
#> [227] "diagnostics.combined.all.stable.ssq"            
#> [228] "diagnostics.combined.all.evolutive.ssm"         
#> [229] "diagnostics.combined.all.evolutive.ssr"         
#> [230] "diagnostics.combined.all.evolutive.ssq"         
#> [231] "diagnostics.combined.end.kruskalwallis"         
#> [232] "diagnostics.combined.end.stable"                
#> [233] "diagnostics.combined.end.evolutive"             
#> [234] "diagnostics.combined.end.summary"               
#> [235] "diagnostics.combined.end.stable.ssm"            
#> [236] "diagnostics.combined.end.stable.ssr"            
#> [237] "diagnostics.combined.end.stable.ssq"            
#> [238] "diagnostics.combined.end.evolutive.ssm"         
#> [239] "diagnostics.combined.end.evolutive.ssr"         
#> [240] "diagnostics.combined.end.evolutive.ssq"         
#> [241] "diagnostics.combined.residual.all.kruskalwallis"
#> [242] "diagnostics.combined.residual.all.stable"       
#> [243] "diagnostics.combined.residual.all.evolutive"    
#> [244] "diagnostics.combined.residual.all.summary"      
#> [245] "diagnostics.combined.residual.all.stable.ssm"   
#> [246] "diagnostics.combined.residual.all.stable.ssr"   
#> [247] "diagnostics.combined.residual.all.stable.ssq"   
#> [248] "diagnostics.combined.residual.all.evolutive.ssm"
#> [249] "diagnostics.combined.residual.all.evolutive.ssr"
#> [250] "diagnostics.combined.residual.all.evolutive.ssq"
#> [251] "diagnostics.combined.residual.end.kruskalwallis"
#> [252] "diagnostics.combined.residual.end.stable"       
#> [253] "diagnostics.combined.residual.end.evolutive"    
#> [254] "diagnostics.combined.residual.end.summary"      
#> [255] "diagnostics.combined.residual.end.stable.ssm"   
#> [256] "diagnostics.combined.residual.end.stable.ssr"   
#> [257] "diagnostics.combined.residual.end.stable.ssq"   
#> [258] "diagnostics.combined.residual.end.evolutive.ssm"
#> [259] "diagnostics.combined.residual.end.evolutive.ssr"
#> [260] "diagnostics.combined.residual.end.evolutive.ssq"
#> [261] "diagnostics.residual.all"                       
#> [262] "diagnostics.residual.end"                       
#> [263] "diagnostics.residualtd"                         
#> [264] "diagnostics.residualtd.on.i"                    
#> [265] "diagnostics.variancedecomposition"              
#> [266] "diagnostics.logstat"                            
#> [267] "diagnostics.levelstat"                          
#> [268] "diagnostics.fcast-insample-mean"                
#> [269] "diagnostics.fcast-outsample-mean"               
#> [270] "diagnostics.fcast-outsample-variance"           
#> [271] "diagnostics.seas-lin-f"                         
#> [272] "diagnostics.seas-lin-qs"                        
#> [273] "diagnostics.seas-lin-kw"                        
#> [274] "diagnostics.seas-lin-friedman"                  
#> [275] "diagnostics.seas-lin-periodogram"               
#> [276] "diagnostics.seas-lin-spectralpeaks"             
#> [277] "diagnostics.seas-si-combined"                   
#> [278] "diagnostics.seas-si-evolutive"                  
#> [279] "diagnostics.seas-si-stable"                     
#> [280] "diagnostics.seas-res-f"                         
#> [281] "diagnostics.seas-res-qs"                        
#> [282] "diagnostics.seas-res-kw"                        
#> [283] "diagnostics.seas-res-friedman"                  
#> [284] "diagnostics.seas-res-periodogram"               
#> [285] "diagnostics.seas-res-spectralpeaks"             
#> [286] "diagnostics.seas-res-combined"                  
#> [287] "diagnostics.seas-res-combined3"                 
#> [288] "diagnostics.seas-res-evolutive"                 
#> [289] "diagnostics.seas-res-stable"                    
#> [290] "diagnostics.seas-i-f"                           
#> [291] "diagnostics.seas-i-qs"                          
#> [292] "diagnostics.seas-i-kw"                          
#> [293] "diagnostics.seas-i-periodogram"                 
#> [294] "diagnostics.seas-i-spectralpeaks"               
#> [295] "diagnostics.seas-i-combined"                    
#> [296] "diagnostics.seas-i-combined3"                   
#> [297] "diagnostics.seas-i-evolutive"                   
#> [298] "diagnostics.seas-i-stable"                      
#> [299] "diagnostics.seas-sa-f"                          
#> [300] "diagnostics.seas-sa-qs"                         
#> [301] "diagnostics.seas-sa-kw"                         
#> [302] "diagnostics.seas-sa-friedman"                   
#> [303] "diagnostics.seas-sa-periodogram"                
#> [304] "diagnostics.seas-sa-spectralpeaks"              
#> [305] "diagnostics.seas-sa-combined"                   
#> [306] "diagnostics.seas-sa-combined3"                  
#> [307] "diagnostics.seas-sa-evolutive"                  
#> [308] "diagnostics.seas-sa-stable"                     
#> [309] "diagnostics.seas-sa-ac1"                        
#> [310] "diagnostics.td-sa-all"                          
#> [311] "diagnostics.td-sa-last"                         
#> [312] "diagnostics.td-i-all"                           
#> [313] "diagnostics.td-i-last"                          
#> [314] "diagnostics.td-res-all"                         
#> [315] "diagnostics.td-res-last"                        
#> [316] "diagnostics.ic-ratio-henderson"                 
#> [317] "diagnostics.ic-ratio"                           
#> [318] "diagnostics.msr-global"                         
#> [319] "diagnostics.msr(*)"                             
#> [320] "coherence.annualtotals.value"                   
#> [321] "coherence.annualtotals"                         
#> [322] "coherence.definition.value"                     
#> [323] "coherence.definition"                           
#> [324] "residuals.normality.value"                      
#> [325] "residuals.normality"                            
#> [326] "residuals.independence.value"                   
#> [327] "residuals.independence"                         
#> [328] "residuals.tdpeaks.value"                        
#> [329] "residuals.tdpeaks"                              
#> [330] "residuals.seaspeaks.value"                      
#> [331] "residuals.seaspeaks"                            
#> [332] "benchmarking.original"                          
#> [333] "benchmarking.target"                            
#> [334] "benchmarking.result"                            

get_indicators(mysa, "decomposition.b2", "decomposition.d10")
#> $decomposition.b2
#>            Jan       Feb       Mar       Apr       May       Jun       Jul
#> 1990                                                              80.81217
#> 1991  79.80106  79.70994  79.67580  79.59134  79.50538  79.47901  79.42114
#> 1992  79.12460  79.05572  78.94483  78.69321  78.52768  78.38786  78.14774
#> 1993  75.90577  75.64151  75.38622  75.15483  74.74513  74.45864  74.50543
#> 1994  75.78817  76.01356  76.27707  76.69293  77.25007  77.93911  78.53318
#> 1995  80.46376  80.67467  80.82205  80.94985  81.04038  81.03817  80.87189
#> 1996  80.71720  80.80987  80.93185  81.01703  81.04874  80.99240  80.97044
#> 1997  82.96634  83.42150  83.91180  84.52530  85.21059  85.84273  86.53911
#> 1998  89.39197  89.70959  89.94590  90.14744  90.35497  90.56634  90.65483
#> 1999  91.68494  91.84151  92.09455  92.46733  92.76597  93.15447  93.70126
#> 2000  96.43072  96.77119  97.04041  97.33407  97.77341  98.14357  98.32554
#> 2001  99.49568  99.71697  99.88142  99.86773  99.71457  99.31793  98.96634
#> 2002  98.11773  97.99744  97.90913  97.83300  97.71788  97.56235  97.40864
#> 2003  96.26634  96.01733  95.82430  95.81697  95.82725  95.85939  95.92661
#> 2004  97.40987  97.59240  97.86924  98.10607  98.12473  98.26210  98.63489
#> 2005  98.82567  98.67189  98.68540  98.59709  98.57507  98.75994  98.77485
#> 2006  99.24709  99.47884  99.58455  99.73318  99.97788  99.99650  99.92606
#> 2007 100.78735 101.13780 101.22309 101.30106 101.48123 101.48876 101.52467
#> 2008 101.17953 100.86024 100.56640 100.09960  99.70514  99.63583  99.32425
#> 2009  95.49335  95.48172  95.65128  95.68191  95.61647  95.36118  95.27884
#> 2010  98.03811  98.34052  98.55189  98.78301  98.91497  99.23265  99.88777
#> 2011 101.50396 101.62936 101.71370 101.83372 102.03670 102.20491 102.15315
#> 2012 101.29141 101.36111 101.28960 101.00371 100.68692 100.27556  99.78270
#> 2013  99.09590  98.91728  98.72897  98.74868  98.78772  98.76135  98.80765
#> 2014  98.58201  98.52467  98.57331  98.55348  98.45543  98.46257  98.51728
#> 2015  98.87015  98.98360  99.24907  99.41728  99.69981  99.95701 100.14134
#> 2016 100.65091 100.54538 100.46192 100.36723 100.26883 100.35471 100.52474
#> 2017 101.28777 101.54868 101.72105 102.10719 102.71022 103.07884 103.15007
#> 2018 103.75302 103.99515 104.01376 103.97923 103.92191 103.80443 103.84451
#> 2019 104.62090 104.58395 104.62481 104.75701 104.63355 104.37385 104.16181
#> 2020 103.61043 103.77713 103.86739 103.67700 103.59975 103.58422 103.49902
#> 2021 102.87236 102.61649 102.44318 102.40254 102.35877 102.37415          
#>            Aug       Sep       Oct       Nov       Dec
#> 1990  80.72092  80.57481  80.37761  79.95447  79.80642
#> 1991  79.31258  79.17659  79.18260  79.42274  79.39140
#> 1992  77.80223  77.33856  76.83957  76.47209  76.16257
#> 1993  74.56176  74.62884  74.77621  74.99568  75.39038
#> 1994  79.03902  79.55030  79.99809  80.21773  80.27290
#> 1995  80.70906  80.64774  80.59556  80.52877  80.60726
#> 1996  81.08645  81.34207  81.73254  82.18911  82.58830
#> 1997  87.21901  87.75070  88.14540  88.57983  88.99930
#> 1998  90.67625  90.75523  90.90207  91.06376  91.38340
#> 1999  94.23108  94.80794  95.34893  95.89637  96.22958
#> 2000  98.59103  98.98077  99.24663  99.19134  99.24705
#> 2001  98.80008  98.65814  98.56511  98.34614  98.17309
#> 2002  97.29076  97.09378  96.97175  96.93077  96.61330
#> 2003  95.98611  96.04220  96.12541  96.41405  96.96983
#> 2004  98.84553  98.79465  98.75869  98.88318  98.96955
#> 2005  98.70568  98.83866  98.96561  98.96356  99.06040
#> 2006 100.07171 100.30161 100.44247 100.47050 100.49705
#> 2007 101.68903 101.68403 101.72731 101.78487 101.53185
#> 2008  98.65558  97.88575  97.03870  96.39804  95.94243
#> 2009  95.46692  95.86673  96.41774  97.00860  97.56574
#> 2010 100.61910 101.23618 101.61689 101.67808 101.51868
#> 2011 101.85923 101.55484 101.40598 101.23693 101.18941
#> 2012  99.51601  99.38632  99.23495  99.17431  99.16793
#> 2013  98.88560  98.90112  98.91659  98.92561  98.75814
#> 2014  98.49302  98.49469  98.55189  98.58717  98.78581
#> 2015 100.27470 100.30268 100.30939 100.54974 100.73075
#> 2016 100.60414 100.77100 100.92295 100.96673 101.06774
#> 2017 103.21238 103.41643 103.57812 103.45284 103.43355
#> 2018 104.09076 104.15886 104.24499 104.67431 104.77626
#> 2019 103.94075 103.79517 103.56296 103.28758 103.40020
#> 2020 103.45236 103.39365 103.38137 103.32283 103.11388
#> 2021                                                  
#> 
#> $decomposition.d10
#>               Jan          Feb          Mar          Apr          May
#> 1990  -3.23112424  -2.45358625   6.92606765   0.46855094  -2.53648128
#> 1991  -3.18607624  -2.56877244   6.76211515   0.48073025  -2.43731681
#> 1992  -2.96230026  -2.81860766   6.50479190   0.50513443  -2.44011384
#> 1993  -2.87063337  -3.12899915   6.34172006   0.56849659  -2.62588295
#> 1994  -2.90970212  -3.39113948   6.26254717   0.65764640  -2.95333714
#> 1995  -3.15354010  -3.54121591   6.35424853   0.70143710  -3.24373983
#> 1996  -3.34181747  -3.66292833   6.55920597   0.65038775  -3.44649460
#> 1997  -3.50678240  -3.81445820   6.94945266   0.53539013  -3.53576744
#> 1998  -3.71883351  -3.93407836   7.54825524   0.34440535  -3.56603122
#> 1999  -3.81010166  -3.95497735   8.28627204   0.04759366  -3.63050145
#> 2000  -3.88282400  -3.88906935   9.10645871  -0.06727057  -3.93623910
#> 2001  -3.92507755  -3.71650232   9.76574512   0.03272906  -4.33189628
#> 2002  -3.91951955  -3.57720406  10.07055976   0.37495154  -4.52547101
#> 2003  -3.72159176  -3.59697554  10.01360691   0.67061526  -4.32561681
#> 2004  -3.48856885  -3.74155605   9.77497323   0.85922176  -3.99056174
#> 2005  -3.27607861  -3.85475066   9.45486880   0.92599515  -3.67421933
#> 2006  -3.14050695  -3.85113453   9.04096804   0.82717345  -3.46594093
#> 2007  -3.15341374  -3.77606532   8.71892996   0.69347864  -3.37908023
#> 2008  -3.18834807  -3.45086967   8.53759913   0.58766908  -3.60423841
#> 2009  -3.17511237  -3.12766081   8.45445778   0.67161637  -4.00750317
#> 2010  -3.04966470  -2.83589556   8.44708199   0.72158415  -4.36870140
#> 2011  -3.01837774  -2.68878555   8.59020442   0.94404638  -4.67678706
#> 2012  -3.09085753  -2.43933782   8.84694402   1.14722039  -5.06210593
#> 2013  -3.19643380  -2.33715168   8.87124254   1.51571104  -5.24700795
#> 2014  -3.27646548  -2.43517696   8.81815223   1.61051043  -4.98222683
#> 2015  -3.41496340  -2.76490101   8.65728424   1.50230186  -4.39258367
#> 2016  -3.45672829  -3.11078319   8.57238852   1.13155806  -3.77217598
#> 2017  -3.50989539  -3.44301963   8.47163668   0.57271598  -3.21746805
#> 2018  -3.59158685  -3.61964964   8.56018364   0.04440789  -2.80790959
#> 2019  -3.80462770  -3.59111017   8.63642758  -0.32962167  -2.63209004
#> 2020  -3.95684375  -3.44658475   8.71390004  -0.40887694  -2.64743506
#>               Jun          Jul          Aug          Sep          Oct
#> 1990   8.58652688  -0.93318080 -26.88627300   5.84425980   9.51277718
#> 1991   8.78444653  -0.96321830 -26.88978248   5.80580137   9.40295915
#> 1992   9.10177488  -0.95685315 -26.87859177   5.74926791   9.19709183
#> 1993   9.58461516  -0.89739294 -26.95134964   5.71343361   9.01884480
#> 1994  10.02989689  -0.72683798 -26.99605412   5.74298632   8.94861147
#> 1995  10.43634302  -0.46190103 -27.25086279   5.82222095   9.03999618
#> 1996  10.73543827  -0.16813261 -27.64165508   5.99403027   9.25566980
#> 1997  10.99323923   0.05291816 -28.13124082   6.10042512   9.50919029
#> 1998  11.09694914   0.22726160 -28.50144380   6.16198789   9.73674073
#> 1999  11.18144533   0.42391323 -28.81976252   6.21380367   9.84430721
#> 2000  11.21797537   0.62328083 -29.09341341   6.38240916   9.99685294
#> 2001  11.36879282   0.74289141 -29.40394895   6.71124769  10.09258545
#> 2002  11.60278864   0.60684880 -29.67420830   7.16980029  10.07521124
#> 2003  11.96015452   0.30360152 -30.00881683   7.69771451   9.86011980
#> 2004  12.31852464   0.09391455 -30.31807523   8.02628768   9.67637687
#> 2005  12.52327924   0.09885612 -30.51238953   8.15681336   9.36344639
#> 2006  12.33958047   0.31153876 -30.20478335   8.06899292   9.05477057
#> 2007  11.88124011   0.60529198 -29.43838637   7.90025983   8.63244476
#> 2008  11.15557250   1.06197675 -28.40162182   7.62353784   8.35573587
#> 2009  10.38873789   1.56844873 -27.26111264   7.44010250   7.86078958
#> 2010   9.78187334   2.00841221 -26.20880904   7.27532429   7.50998794
#> 2011   9.33578933   2.39261457 -25.31053420   7.15696114   7.18826481
#> 2012   9.13588277   2.72058362 -24.63099553   6.91117326   7.20147554
#> 2013   8.96813476   2.91687978 -24.08100452   6.71982618   7.09666821
#> 2014   8.87528633   2.72180065 -23.74022571   6.47653745   7.31380776
#> 2015   8.80293789   2.44110955 -23.51700294   6.18755382   7.53213155
#> 2016   8.83655120   2.15132750 -23.48623552   5.88676109   8.01056701
#> 2017   8.93946680   2.18514995 -23.34438622   5.62725179   8.32254026
#> 2018   9.09029550   2.32669134 -23.23570602   5.45119622   8.74335446
#> 2019   9.27156738   2.67473456 -23.03712953   5.35076837   8.94170126
#> 2020   9.41303027   2.92492541 -22.88952482   5.40065806   9.07499614
#>               Nov          Dec
#> 1990   3.27525681   1.47198330
#> 1991   3.15895332   1.71980899
#> 1992   3.01106153   2.16973476
#> 1993   2.82218126   2.63980962
#> 1994   2.55444586   2.96552928
#> 1995   2.35284825   3.01697689
#> 1996   2.19656043   2.85046082
#> 1997   2.27065604   2.51098356
#> 1998   2.35882014   1.97624777
#> 1999   2.50690433   1.30097501
#> 2000   2.51666198   0.48630618
#> 2001   2.42153335  -0.29313541
#> 2002   2.20230841  -0.88637417
#> 2003   2.06488215  -1.20658494
#> 2004   2.01191290  -1.37471507
#> 2005   2.18210642  -1.31799891
#> 2006   2.56173475  -1.37520844
#> 2007   2.91907983  -1.56835084
#> 2008   3.09774192  -1.88197812
#> 2009   3.05421329  -2.12864166
#> 2010   2.79143000  -2.39700685
#> 2011   2.35016391  -2.67559624
#> 2012   1.89569400  -2.89923014
#> 2013   1.64129678  -2.89157726
#> 2014   1.74059501  -2.80060355
#> 2015   2.05495041  -2.75281805
#> 2016   2.44475876  -2.84265268
#> 2017   2.74794776  -3.25879500
#> 2018   2.87928835  -3.86713780
#> 2019   2.82444428  -4.53979302
#> 2020   2.63661191  -5.03889824
#> 

# To convert the Java object to an R object
jSA2R(mysa)
#> RegARIMA
#> y = regression model + arima (2, 1, 1, 0, 1, 1)
#> Log-transformation: no
#> Coefficients:
#>             Estimate Std. Error
#> Phi(1)     0.0003269      0.108
#> Phi(2)     0.1688192      0.074
#> Theta(1)  -0.5485606      0.102
#> BTheta(1) -0.6660849      0.042
#> 
#>               Estimate Std. Error
#> Monday         0.55932      0.228
#> Tuesday        0.88221      0.228
#> Wednesday      1.03996      0.229
#> Thursday       0.04943      0.229
#> Friday         0.91132      0.230
#> Saturday      -1.57769      0.228
#> Leap year      2.15403      0.705
#> Easter [1]    -2.37950      0.454
#> TC (4-2020)  -35.59245      2.173
#> AO (3-2020)  -20.89026      2.180
#> AO (5-2011)   13.49850      1.857
#> LS (11-2008) -12.54901      1.636
#> 
#> 
#> Residual standard error: 2.218 on 342 degrees of freedom
#> Log likelihood = -799.1, aic =  1632 aicc =  1634, bic(corrected for length) = 1.855
#> 
#> 
#> 
#> Decomposition
#> Monitoring and Quality Assessment Statistics:
#>       M stats
#> M(1)    0.163
#> M(2)    0.089
#> M(3)    1.181
#> M(4)    0.558
#> M(5)    1.020
#> M(6)    0.090
#> M(7)    0.083
#> M(8)    0.244
#> M(9)    0.062
#> M(10)   0.272
#> M(11)   0.256
#> Q       0.368
#> Q-M2    0.402
#> 
#> Final filters: 
#> Seasonal filter:  3x5
#> Trend filter:  13 terms Henderson moving average
#> 
#> 
#> Final
#> Last observed values
#>              y        sa        t            s             i
#> Jan 2020 101.0 102.95613 102.9586  -1.95613209  -0.002494203
#> Feb 2020 100.1 103.50876 102.9592  -3.40875640   0.549602816
#> Mar 2020  91.8  82.87617 103.1664   8.92382800 -20.290271773
#> Apr 2020  66.7  66.65243 103.5971   0.04756625 -36.944710027
#> May 2020  73.7  78.87836 104.0393  -5.17835604 -25.160905985
#> Jun 2020  98.2  87.34544 104.3804  10.85456021 -17.034985133
#> Jul 2020  97.4  92.47436 104.5319   4.92563707 -12.057551871
#> Aug 2020  71.7  97.47245 104.3751 -25.77244698  -6.902636199
#> Sep 2020 104.7  97.37717 103.9182   7.32282919  -6.541070626
#> Oct 2020 106.7  98.24194 103.3047   8.45805540  -5.062719500
#> Nov 2020 101.6 100.26862 102.7746   1.33138152  -2.506014899
#> Dec 2020  96.6  99.66730 102.5133  -3.06729670  -2.845961796
#> 
#> Forecasts:
#>                y_f     sa_f      t_f          s_f        i_f
#> Jan 2021  94.53021 101.0902 102.4794  -6.56002888 -1.3891608
#> Feb 2021  97.90024 101.7395 102.5246  -3.83928384 -0.7850772
#> Mar 2021 114.09983 102.3065 102.5087  11.79328397 -0.2021598
#> Apr 2021 102.16781 102.2220 102.3759  -0.05422341 -0.1538967
#> May 2021  96.01612 101.5450 102.2100  -5.52888123 -0.6650098
#> Jun 2021 112.76658 101.3438 102.0725  11.42275939 -0.7286526
#> Jul 2021 104.13805 101.6681 102.0297   2.46989932 -0.3615193
#> Aug 2021  79.13003 102.3617 102.1360 -23.23171595  0.2257112
#> Sep 2021 109.06438 102.4772 102.3249   6.58713572  0.1523168
#> Oct 2021 108.64207 102.1329 102.5185   6.50921416 -0.3856588
#> Nov 2021 106.46022 102.5908 102.6996   3.86943752 -0.1088338
#> Dec 2021  99.79901 103.0831 102.8580  -3.28410831  0.2251086
#> 
#> 
#> Diagnostics
#> Relative contribution of the components to the stationary
#> portion of the variance in the original series,
#> after the removal of the long term trend
#>  Trend computed by Hodrick-Prescott filter (cycle length = 8.0 years)
#>            Component
#>  Cycle         2.251
#>  Seasonal     59.750
#>  Irregular     1.067
#>  TD & Hol.     2.610
#>  Others       33.718
#>  Total        99.395
#> 
#> Combined test in the entire series
#>  Non parametric tests for stable seasonality
#>                                                           P.value
#>    Kruskall-Wallis test                                      0.000
#>    Test for the presence of seasonality assuming stability   0.000
#>    Evolutive seasonality test                                0.034
#>  
#>  Identifiable seasonality present
#> 
#> Residual seasonality tests
#>                                       P.value
#>  qs test on sa                          0.985
#>  qs test on i                           0.865
#>  f-test on sa (seasonal dummies)        0.958
#>  f-test on i (seasonal dummies)         0.893
#>  Residual seasonality (entire series)   0.876
#>  Residual seasonality (last 3 years)    0.906
#>  f-test on sa (td)                      0.987
#>  f-test on i (td)                       0.993
#> 
#> 
#> Additional output variables
```
