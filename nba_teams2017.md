---
title: "nba_teams2017"
author: "Julien Jaber"
date: "7/2/2018"
output: 
  html_document: 
    keep_md: yes
---





```r
nba_teams_2017 <- read.file("/Users/julienjaber/Desktop/Classes/Spring 2018/STAT 154/stat_154/datasets/nba-teams-2017.csv")
```

```
## Reading data with read.csv()
```

```r
teams = nba_teams_2017$team
nba_teams_2017$team = NULL
nba_teams_2017$games_played = NULL

rownames(nba_teams_2017) = teams
kable(head(nba_teams_2017))
```

                         wins   losses   win_prop   minutes   points   field_goals   field_goals_attempted   field_goals_prop   points3   points3_attempted   points3_prop   free_throws   free_throws_att   free_throws_prop   off_rebounds   def_rebounds   rebounds   assists   turnovers   steals   blocks   block_fga   personal_fouls   personal_fouls_drawn   plus_minus
----------------------  -----  -------  ---------  --------  -------  ------------  ----------------------  -----------------  --------  ------------------  -------------  ------------  ----------------  -----------------  -------------  -------------  ---------  --------  ----------  -------  -------  ----------  ---------------  ---------------------  -----------
Golden State Warriors      67       15      0.817      48.2    115.9          43.1                    87.1               49.5      12.0                31.2           38.3          17.8              22.6               78.8            9.4           35.0       44.4      30.4        14.8      9.6      6.8         3.8             19.3                   19.4         11.6
San Antonio Spurs          61       21      0.744      48.3    105.3          39.3                    83.7               46.9       9.2                23.5           39.1          17.6              22.0               79.7           10.0           33.9       43.9      23.8        13.4      8.0      5.9         4.1             18.3                   19.8          7.2
Houston Rockets            55       27      0.671      48.2    115.3          40.3                    87.2               46.2      14.4                40.3           35.7          20.3              26.5               76.6           10.9           33.5       44.4      25.2        15.1      8.2      4.3         5.0             19.9                   20.4          5.8
Boston Celtics             53       29      0.646      48.2    108.0          38.6                    85.1               45.4      12.0                33.4           35.9          18.7              23.2               80.7            9.1           32.9       42.0      25.2        13.3      7.5      4.1         5.2             20.6                   20.3          2.6
Utah Jazz                  51       31      0.622      48.2    100.7          37.0                    79.5               46.6       9.6                26.0           37.2          17.1              22.9               74.7            9.4           33.8       43.2      20.1        13.6      6.7      5.0         3.8             18.8                   20.2          3.9
Toronto Raptors            51       31      0.622      48.2    106.9          39.2                    84.4               46.4       8.8                24.3           36.3          19.7              24.7               79.6           10.6           32.6       43.3      18.5        12.7      8.3      4.9         4.8             20.8                   20.3          4.2

```r
kable(summary(nba_teams_2017))
```

          wins           losses         win_prop        minutes          points       field_goals    field_goals_attempted   field_goals_prop      points3      points3_attempted    points3_prop    free_throws    free_throws_att   free_throws_prop    off_rebounds     def_rebounds      rebounds        assists        turnovers         steals          blocks        block_fga     personal_fouls   personal_fouls_drawn     plus_minus 
---  --------------  --------------  --------------  --------------  --------------  --------------  ----------------------  -----------------  --------------  ------------------  --------------  --------------  ----------------  -----------------  ---------------  --------------  --------------  --------------  --------------  --------------  --------------  --------------  ---------------  ---------------------  -------------
     Min.   :20.00   Min.   :15.00   Min.   :0.244   Min.   :48.10   Min.   : 97.9   Min.   :36.20   Min.   :79.50           Min.   :43.50      Min.   : 7.30   Min.   :21.00       Min.   :32.70   Min.   :13.90   Min.   :18.50     Min.   :70.60      Min.   : 7.900   Min.   :30.70   Min.   :38.60   Min.   :18.50   Min.   :11.50   Min.   :6.600   Min.   :3.700   Min.   :3.100   Min.   :16.60    Min.   :17.50          Min.   :-6.9 
     1st Qu.:32.25   1st Qu.:31.50   1st Qu.:0.393   1st Qu.:48.20   1st Qu.:103.0   1st Qu.:38.15   1st Qu.:84.40           1st Qu.:44.75      1st Qu.: 8.65   1st Qu.:24.00       1st Qu.:34.23   1st Qu.:17.02   1st Qu.:22.10     1st Qu.:74.85      1st Qu.: 9.025   1st Qu.:32.67   1st Qu.:42.83   1st Qu.:21.12   1st Qu.:13.30   1st Qu.:7.125   1st Qu.:4.125   1st Qu.:4.375   1st Qu.:18.88    1st Qu.:19.32          1st Qu.:-2.7 
     Median :41.00   Median :41.00   Median :0.500   Median :48.30   Median :105.0   Median :39.25   Median :85.35           Median :45.45      Median : 9.30   Median :26.10       Median :35.60   Median :17.95   Median :23.05     Median :77.55      Median :10.050   Median :33.40   Median :43.60   Median :22.50   Median :13.75   Median :7.800   Median :4.800   Median :4.950   Median :20.00    Median :19.85          Median : 0.0 
     Mean   :41.00   Mean   :41.00   Mean   :0.500   Mean   :48.32   Mean   :105.6   Mean   :39.05   Mean   :85.42           Mean   :45.72      Mean   : 9.65   Mean   :27.00       Mean   :35.72   Mean   :17.83   Mean   :23.11     Mean   :77.18      Mean   :10.133   Mean   :33.38   Mean   :43.52   Mean   :22.63   Mean   :13.96   Mean   :7.710   Mean   :4.740   Mean   :4.747   Mean   :19.89    Mean   :19.91          Mean   : 0.0 
     3rd Qu.:50.50   3rd Qu.:49.75   3rd Qu.:0.616   3rd Qu.:48.40   3rd Qu.:107.8   3rd Qu.:39.58   3rd Qu.:87.10           3rd Qu.:46.67      3rd Qu.:10.38   3rd Qu.:28.75       3rd Qu.:37.20   3rd Qu.:19.07   3rd Qu.:24.20     3rd Qu.:79.40      3rd Qu.:11.050   3rd Qu.:34.33   3rd Qu.:44.38   3rd Qu.:23.77   3rd Qu.:14.95   3rd Qu.:8.200   3rd Qu.:5.000   3rd Qu.:5.200   3rd Qu.:20.77    3rd Qu.:20.40          3rd Qu.: 2.4 
     Max.   :67.00   Max.   :62.00   Max.   :0.817   Max.   :48.60   Max.   :115.9   Max.   :43.10   Max.   :88.80           Max.   :49.50      Max.   :14.40   Max.   :40.30       Max.   :39.10   Max.   :20.40   Max.   :26.50     Max.   :81.50      Max.   :12.200   Max.   :35.10   Max.   :46.60   Max.   :30.40   Max.   :16.70   Max.   :9.600   Max.   :6.800   Max.   :5.600   Max.   :24.80    Max.   :22.40          Max.   :11.6 


**prcomp performs PCA on data matrix and returns result as an object of class prcomp. Calculation is done by SVD**


```r
X = nba_teams_2017
pca1 <- prcomp(X,
              center = TRUE,
              scale. = TRUE) 

eigenvalues1 = pca1$sdev^2

#these are the first 5 principal components
scores1 = data.frame(pca1$x)
kable(head(scores1[, 1:5]))
```

                                PC1          PC2          PC3         PC4         PC5
----------------------  -----------  -----------  -----------  ----------  ----------
Golden State Warriors    -8.3302687    0.4765724   -1.9924008   -1.605765   -2.762683
San Antonio Spurs        -3.6130556   -1.9910936   -0.8131246   -1.668764    1.028205
Houston Rockets          -4.5394019    2.6912271    1.1000921    2.606653   -1.245341
Boston Celtics           -2.0574221   -0.5751060    1.7435372    1.365106   -1.045489
Utah Jazz                -0.8921328   -3.1495001    0.5074295    0.459024    2.500746
Toronto Raptors          -1.2655459    0.0801278    1.1037663   -1.836868    1.721321

```r
#proportion of total variance explained by first 5 PCs
prop.pca1 = pca1$sdev^2/sum(pca1$sdev^2)
(prop.pca1*100)[1:5]
```

```
## [1] 29.026037 17.202726 12.054088  8.808959  7.247320
```



```r
#Eigenvalues represent variance. Adding up all eigenvalues should give you an output = p, the number of predictors

total_eigenvalues = sum(eigenvalues1)
total_eigenvalues
```

```
## [1] 25
```

```r
round(total_eigenvalues, 3) == ncol(X)
```

```
## [1] TRUE
```



**We see that eigenvalues 1 and 2 explain over 46% of total variance**

**Also the last 8 PCs are useless to include in our study as they explain no variation at all**


```r
eigenvalues1 = round(data.frame(eigenvalues1), 2)
eigenvalues1 <- eigenvalues1 %>%
  mutate(perc_variance = round(100* eigenvalues1/total_eigenvalues, 2)) %>%
  mutate(cumulative = round(cumsum(perc_variance), 2))


colnames(eigenvalues1) = c("eigenvalue", "variance(%)", "cumulative(%)")
kable(eigenvalues1)
```



 eigenvalue   variance(%)   cumulative(%)
-----------  ------------  --------------
       7.26         29.04           29.04
       4.30         17.20           46.24
       3.01         12.04           58.28
       2.20          8.80           67.08
       1.81          7.24           74.32
       1.29          5.16           79.48
       1.14          4.56           84.04
       1.00          4.00           88.04
       0.86          3.44           91.48
       0.60          2.40           93.88
       0.56          2.24           96.12
       0.35          1.40           97.52
       0.25          1.00           98.52
       0.17          0.68           99.20
       0.09          0.36           99.56
       0.07          0.28           99.84
       0.04          0.16          100.00
       0.00          0.00          100.00
       0.00          0.00          100.00
       0.00          0.00          100.00
       0.00          0.00          100.00
       0.00          0.00          100.00
       0.00          0.00          100.00
       0.00          0.00          100.00
       0.00          0.00          100.00

**The Scree plot is a way to decide how many PCs we want to keep (elbow method). Here we might deduce that 6 PCs might be enough**


```r
fviz_eig(pca1, addlabels = TRUE, ylim = c(0, 50))
```

![](nba_teams2017_files/figure-html/unnamed-chunk-6-1.png)<!-- -->

**We can also decide on the number of PCs to use in our analysis based on Kaiser's rule which says that we only include eigenvalues that are > 1, so in this case 7 PCs. After that, PCs don't show that much variation so you can exclude them**



```r
number_PCA_chosen <- eigenvalues1 %>%
 filter(eigenvalue > 1)

kable(number_PCA_chosen)
```



 eigenvalue   variance(%)   cumulative(%)
-----------  ------------  --------------
       7.26         29.04           29.04
       4.30         17.20           46.24
       3.01         12.04           58.28
       2.20          8.80           67.08
       1.81          7.24           74.32
       1.29          5.16           79.48
       1.14          4.56           84.04



# Studying the cloud of individuals

**Displaying only 1st and 2nd PCs for easy visualization**


```r
plot(scores1$PC1, scores1$PC2, type = "n", main = "Scatter of teams on PC1 and PC2", xlab = "PC1", ylab = "PC2")
text(x=scores1$PC1, y=scores1$PC2, labels=teams, cex = 0.7)
abline(h = 0, v = 0)
```

![](nba_teams2017_files/figure-html/unnamed-chunk-8-1.png)<!-- -->

From this graph, we can see that Golden State Warriors is clearly a stand out team, with the Houston Rockets being the closest to it.

PC1 shows most variability.

PC2 still depicts a good amount of variability, but less overall variability than PC1.


### Quality of representation on first two Dimensions



```r
library("corrplot")
```

```
## corrplot 0.84 loaded
```

```r
ind <- get_pca_ind(pca1)

quality_PC1_PC2 = ind$cos2[, 1:2]
kable(quality_PC1_PC2)
```

                              Dim.1       Dim.2
-----------------------  ----------  ----------
Golden State Warriors     0.7988437   0.0026146
San Antonio Spurs         0.5249844   0.1594338
Houston Rockets           0.4747201   0.1668557
Boston Celtics            0.2554982   0.0199635
Utah Jazz                 0.0334681   0.4171149
Toronto Raptors           0.1082331   0.0004339
Cleveland Cavaliers       0.3469252   0.0327792
LA Clippers               0.3651131   0.0221366
Washington Wizards        0.2522167   0.0023667
Oklahoma City Thunder     0.0001138   0.6129988
Memphis Grizzlies         0.1485320   0.0176157
Atlanta Hawks             0.0056472   0.1083799
Indiana Pacers            0.0052437   0.1500286
Milwaukee Bucks           0.0065591   0.3364318
Chicago Bulls             0.0641959   0.0192958
Portland Trail Blazers    0.0013314   0.0451451
Miami Heat                0.0244976   0.0890453
Denver Nuggets            0.1359294   0.3093149
Detroit Pistons           0.1510599   0.0619610
Charlotte Hornets         0.0262883   0.0159454
New Orleans Pelicans      0.0584271   0.0466411
Dallas Mavericks          0.1556605   0.6273338
Sacramento Kings          0.1892487   0.0898835
Minnesota Timberwolves    0.1100059   0.0400606
New York Knicks           0.3139152   0.0262245
Orlando Magic             0.7048125   0.0198914
Philadelphia 76ers        0.3473091   0.0520101
Los Angeles Lakers        0.4579665   0.0707967
Phoenix Suns              0.1850088   0.5743703
Brooklyn Nets             0.2540781   0.1834949

**Comments**

GSW best represented by PC1 (quality = 0.799)

Dallas maverics best represented by PC2 (quality = 0.627)

OKC Worst represented by PC1 is (quality = 0.0033)

Toronto Raptors worst represented by PC2 (quality = 0.0004)


```r
fviz_pca_ind(pca1, col.ind = "cos2", 
             gradient.cols = c("#00AFBB", "#E7B800", "#FC4E07"),
             repel = TRUE # Avoid text overlapping (slow if many points)
             )
```

![](nba_teams2017_files/figure-html/unnamed-chunk-10-1.png)<!-- -->

```r
corrplot(ind$cos2, is.corr=FALSE) 
```

![](nba_teams2017_files/figure-html/unnamed-chunk-10-2.png)<!-- -->

```r
#quality of representation on first two PCs
fviz_cos2(pca1, choice = "ind", axes = 1:2)
```

![](nba_teams2017_files/figure-html/unnamed-chunk-10-3.png)<!-- -->















### Contributions: How much does each observation contribute to the PC


```r
# Contributions to the principal components
kable(ind$contrib[, 1:2])
```

                               Dim.1        Dim.2
-----------------------  -----------  -----------
Golden State Warriors     31.8763806    0.1760351
San Antonio Spurs          5.9965337    3.0727328
Houston Rockets            9.4656023    5.6136091
Boston Celtics             1.9444546    0.2563523
Utah Jazz                  0.3656032    7.6882008
Toronto Raptors            0.7357102    0.0049763
Cleveland Cavaliers        3.9664200    0.6323408
LA Clippers                4.5936838    0.4699328
Washington Wizards         1.5329555    0.0242715
Oklahoma City Thunder      0.0010351    9.4093086
Memphis Grizzlies          1.1992929    0.2399913
Atlanta Hawks              0.0397579    1.2874478
Indiana Pacers             0.0202715    0.9786136
Milwaukee Bucks            0.0466299    4.0356072
Chicago Bulls              0.4864521    0.2467092
Portland Trail Blazers     0.0061156    0.3498979
Miami Heat                 0.1729142    1.0604936
Denver Nuggets             1.2352648    4.7428334
Detroit Pistons            2.7882130    1.9296801
Charlotte Hornets          0.2425001    0.2481840
New Orleans Pelicans       0.3607625    0.4859220
Dallas Mavericks           3.7857445   25.7431654
Sacramento Kings           1.3843446    1.1093841
Minnesota Timberwolves     0.8343197    0.5126538
New York Knicks            2.4030230    0.3387225
Orlando Magic              6.0074826    0.2860710
Philadelphia 76ers         3.2372962    0.8179838
Los Angeles Lakers         4.6404034    1.2103913
Phoenix Suns               3.6825072   19.2900670
Brooklyn Nets              3.6149921    4.4050875



**Contributions of variables to PCs**


```r
kable(head(ind$contrib))
```

                              Dim.1       Dim.2       Dim.3        Dim.4       Dim.5       Dim.6       Dim.7       Dim.8       Dim.9      Dim.10      Dim.11      Dim.12      Dim.13       Dim.14      Dim.15       Dim.16      Dim.17     Dim.18      Dim.19       Dim.20      Dim.21      Dim.22      Dim.23      Dim.24      Dim.25
----------------------  -----------  ----------  ----------  -----------  ----------  ----------  ----------  ----------  ----------  ----------  ----------  ----------  ----------  -----------  ----------  -----------  ----------  ---------  ----------  -----------  ----------  ----------  ----------  ----------  ----------
Golden State Warriors    31.8763806   0.1760351   4.3909426    3.9028182   14.041823   2.9953825   0.5570070   2.2868622   0.2417300   0.9275492   3.9500407   0.1327370   0.1738135    0.3325205   0.0818553    1.9784811   4.3170246   4.595345   1.7413285    0.2766024   9.0901522   0.4772128   0.1113918   0.0027631   223.35043
San Antonio Spurs         5.9965337   3.0727328   0.7313387    4.2150605    1.945005   3.2485864   0.6795358   1.5211764   0.0063738   2.4623762   0.5547644   5.1746698   0.5983173    0.0244873   1.3832387   10.6256683   1.3724492   5.267147   0.0001454   16.6006046   2.6081199   2.6836322   0.3228916   2.4686076   811.26934
Houston Rockets           9.4656023   5.6136091   1.3386358   10.2844407    2.853236   8.2332779   0.8755812   1.8175587   3.1202820   0.1503491   0.2262242   1.3239443   1.4863429   13.9021763   0.0706267    4.8505702   2.1430534   7.406354   2.6933033    3.1847644   1.7856120   1.5467706   0.0369636   3.1811336    21.35774
Boston Celtics            1.9444546   0.2563523   3.3625348    2.8206364    2.010945   2.0901025   7.6674905   1.0650540   1.8297018   0.0164560   0.3190966   0.6480458   0.0006340   29.8398700   0.5739772    2.0277047   3.5417083   0.605475   4.1010804    1.9229722   0.2776899   2.5718145   0.6758466   0.3460196   170.21542
Utah Jazz                 0.3656032   7.6882008   0.2848104    0.3189223   11.505365   0.3784447   5.8986666   4.6675174   2.3470994   7.0711533   0.7846690   4.5031932   0.1206344    0.1758039   3.3704286    8.5097219   0.6848509   4.499416   2.0319010    0.5396383   3.6748077   0.8780732   0.5614177   5.9564322   169.58495
Toronto Raptors           0.7357102   0.0049763   1.3475927    5.1070477    5.451111   2.7622067   3.8702448   0.9861948   0.0911561   3.5197455   3.1714543   6.9643558   8.5502569    6.0183313   2.0353940    0.0316524   1.4805947   2.116065   1.2989482   10.5907366   1.2762451   0.4441807   0.8651975   7.0248675   126.95726

```r
# Aggregate contributions of variables to PC1 and PC2
fviz_contrib(pca1, choice = "ind", axes = 1:2, top = 10)
```

![](nba_teams2017_files/figure-html/unnamed-chunk-12-1.png)<!-- -->


# Studying Variables



```r
var <- get_pca_var(pca1)

# Coordinates
kable(head(var$coord)[, 1:5])
```

                    Dim.1        Dim.2        Dim.3        Dim.4        Dim.5
------------  -----------  -----------  -----------  -----------  -----------
wins           -0.9117736   -0.1919166   -0.0620135   -0.0689162    0.2034957
losses          0.9117736    0.1919166    0.0620135    0.0689162   -0.2034957
win_prop       -0.9120512   -0.1913365   -0.0623882   -0.0688130    0.2036741
minutes         0.1735752    0.0684077    0.1232267    0.0507055    0.1801032
points         -0.7675014    0.5245213    0.0239508    0.1092877   -0.1832465
field_goals    -0.6119886    0.4302333   -0.4179337   -0.2072492   -0.2077184

**Correlation circle - The correlation between a variable and a principal component (PC)**


```r
fviz_pca_var(pca1, col.var = "black")
```

![](nba_teams2017_files/figure-html/unnamed-chunk-14-1.png)<!-- -->

**Positively correlated variables are grouped together**

**Negatively correlated variables are positioned on opposite sides of the plot origin (opposed quadrants)**

**Variables that are away from the origin are well represented on the map**

As expected some variables (wins, losses) will be symmetrical opposite of each other by origin
