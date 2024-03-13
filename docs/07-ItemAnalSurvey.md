# Item Analysis for Likert Type Scale Construction {#ItemAnalSurvey}

 [Screencasted Lecture Link](https://spu.hosted.panopto.com/Panopto/Pages/Viewer.aspx?pid=09cc7469-de42-4288-ad39-ad9e01650656) 
 


The focus of this lecture is on item analysis for surveys. We use information about alpha coefficients and item-total correlations (within and across subscales) to help assess what we might consider to be *within-scale convergent and discriminant validity* (although we tend to think of it as an assessment of reliability).

## Navigating this Lesson

There is about 45 minutes of lecture.  If you work through the materials with me it would be plan for an additional hour.

While the majority of R objects and data you will need are created within the R script that sources the chapter, occasionally there are some that cannot be created from within the R framework. Additionally, sometimes links fail.  All original materials are provided at the [Github site](https://github.com/lhbikos/ReC_Psychometrics) that hosts the book. More detailed guidelines for ways to access all these materials are provided in the OER's [introduction](#ReCintro)

### Learning Objectives

Focusing on this week's materials, make sure you can:

* Define the corrected item-total correlation and compare it to an item-total correlation.
* List the preliminary steps essential for scale construction, beginning with item development.
* Name the type(s; e.g., reliability, validity) of psychometric evaluation that item analytic procedures assess.
* Identify threats to the interpretation of item-total correlations and alpha coefficients.
* Make decisions about item retention, deletion, and revision that balances statistical output with construct definitions.

### Planning for Practice

In each of these lessons I provide suggestions for practice that allow you to select one or more problems that are graded in difficulty. For this lesson, please locate item-level data for a scale that has the potential for at least two subscales  and a total-scale score. Ideally, the data you utilized in one or more of the prior lessons (e.g., changing the random seed in the lesson data, downloading the data from the *ReCentering Psych Stats* survey, or data you found elsewhere) will allow you to continue with these analyses.  Then, please examine the following:

* Produce alpha coefficients, average inter-item correlations, and corrected item-total correlations for the total and subscales, separately.
* Produce correlations between the individual items of one subscale and the subscale scores of all other scales.
* Draft an APA style results section with an accompanying table.

In my example there were only two subscales. If you have more, you will need to compare each subscale with all the others. For example, if you had three subscales:  A, B, C, you would need to compare A/B, B/C, and A/C.

### Readings & Resources

In preparing this chapter, I drew heavily from the following resource(s). Other resources are cited (when possible, linked) in the text with complete citations in the reference list.

* Green & Salkind (2017). Lesson 38: Item analysis using the reliability Procedure. In S.B. Green and N.J. Salkind's, "Using SPSS for Windows and Macintosh: Analyzing and understanding data (8th ed). New York: Pearson.
  - Even though the operation of the chapter uses SPSS, the narration of the "what" and "why" of item analysis is clear and concise. Further, I have not found another chapter (not even in psychometrics texts) that addresses this as completely.
* Szymanski, D. M., & Bissonette, D. (2020). Perceptions of the LGBTQ College Campus Climate Scale: Development and psychometric evaluation. *Journal of Homosexuality*, 67(10), 1412–1428. https://doi.org/10.1080/00918369.2019.1591788
  - The research vignette for this lesson.

### Packages

The packages used in this lesson are embedded in this code. When the hashtags are removed, the script below will (a) check to see if the following packages are installed on your computer and, if not (b) install them.

```r
# will install the package if not already installed
# if(!require(tidyverse)){install.packages('tidyverse')}
# if(!require(MASS)){install.packages('MASS')}
# if(!require(psych)){install.packages('psych')}
# if(!require(apaTables)){install.packages('apaTables')}
# if(!require(sjstats)){install.packages('sjstats')}
# if(!require(qualtRics)){install.packages('qualtRics')}
```

## Intro to Item Analysis for Survey Development

Item analysis can be used to decide which items to include and exclude from a scale or subscale.  The goal is to select a set of items that yields a summary score (total or mean) that is strongly related to the construct identified and defined in the scale. 

* Item analysis is somewhat limiting because we usually cannot relate our items to a direct (external) measure of a construct to select our items.
* Instead, we *trust* (term used lightly) that the items we have chosen, together, represent the construct and we make decisions about the relative strength of each item's correlation to the total score.
* This makes it imperative that we look to both statistics and our construct definition (e.g., how well does each item map onto the construct definition)

## Research Vignette

The research vignette for this lesson is the development and psychometric evaluation of the Perceptions of the LGBTQ College Campus Climate Scale [@szymanski_perceptions_2020]. The scale is six items with responses rated on a 7-point Likert scale ranging from 1 (*strongly disagree*) to 7 (*strongly agree*). Higher scores indicate more negative perceptions of the LGBTQ campus climate. Szymanski and Bissonette have suggested that the psychometric evaluation supports using the scale in its entirety or as subscales composed of the following items:

* College response to LGBTQ students:  
  - My university/college is cold and uncaring toward LGBTQ students. 
  - My university/college is unresponsive to the needs of LGBTQ students. 
  - My university/college provides a supportive environment for LGBTQ students. [un]supportive; must be reverse-scored 
* LGBTQ Stigma:  
  - Negative attitudes toward LGBTQ persons are openly expressed on my university/college campus. 
  - Heterosexism, homophobia, biphobia, transphobia, and cissexism are visible on my university/college campus. 
  - LGBTQ students are harassed on my university/college campus. 

A [preprint](https://www.researchgate.net/publication/332062781_Perceptions_of_the_LGBTQ_College_Campus_Climate_Scale_Development_and_Psychometric_Evaluation/link/5ca0bef945851506d7377da7/download) of the article is available at ResearchGate. 

Because data is collected at the item level (and I want this resource to be as practical as possible, I have simulated the data for each of the scales at the item level. 

Simulating the data involved using factor loadings, means, standard deviations, and correlations between the scales. Because the simulation will produce "out-of-bounds" values, the code below rescales the scores into the range of the Likert-type scaling and rounds them to whole values.

Five additional scales were reported in the Szymanski and Bissonette article [-@szymanski_perceptions_2020]. Unfortunately, I could not load factor loadings for all of them; and in two cases, I used estimates from a more recent psychometric analysis. When the individual item and their factor loadings are known, I assigned names based on item content (e.g., "lo_energy") rather than using item numbers (e.g., "PHQ4"). When I am doing psychometric analyses, I prefer item-level names so that I can quickly see (without having to look up the item names) how the items are behaving. While the focus of this series of chapters is on the LGBTQ Campus Climate scale, this simulated data might be useful to you in one or more of the suggestions for practice (e.g., examining the psychometric characteristics of one or the other scales). The scales, their original citation, and information about how I simulated data for each are listed below.

* **Sexual Orientation-Based Campus Victimization Scale** [@herek_documenting_1993] is a 9-item item scale with Likert scaling ranging from 0 (*never*) to 3 (*two or more times*). Because I was not able to retrieve and inspect the source article in time to write this lesson, I simulated the data by specifying a 0.8 as a standardized factor loading for each of the items.
* **College Satisfaction Scale** [@helm_relationship_1998] is a 5-item scale with Likert scaling ranging from 1 (*strongly disagree*) to 7 (*strongly agree*). Higher scores represent greater college satisfaction. Because I was not able to retrieve and inspect the source article in time to write this lesson, I simulated the data by specifying a 0.8 as a standardized factor loading for each of the items.
* **Institutional and Goals Commitment** [@pascarella_predicting_1980] is a 6-item subscale from a 35-item measure assessing academic/social integration and institutional/goal commtiment (5 subscales total). The measure had with Likert scaling ranging from 1 (*strongly disagree*) to 5 (*strongly agree*). Higher scores on the institutional and goals commitment subscale indicate greater intentions to persist in college. Data were simulated using factor loadings in the source article.
* **GAD-7** [@spitzer_brief_2006] is a 7-item scale with Likert scaling ranging from 0 (*not at all*) to 3 (*nearly every day*). Higher scores indicate more anxiety. I simulated data by estimating factor loadings from Brattmyr et al. [-@brattmyr_factor_2022].
* **PHQ-9** [@kroenke_phq-9_2001] is a 9-item scale with Likert scaling ranging from 0 (*not at all*) to 3 (*nearly every day*). Higher scores indicate higher levels of depression. I simulated data by estimating factor loadings from Brattmyr et al. [-@brattmyr_factor_2022].


```r
#Entering the intercorrelations, means, and standard deviations from the journal article

Szymanski_generating_model <- '
        #measurement model
        CollegeResponse  =~ .88*cold + .73*unresponsive + .73*supportive 
        Stigma =~ .86*negative + .76*heterosexism + .71*harassed
        Victimization =~ .8*Vic1 + .8*Vic2 + .8*Vic3 + .8*Vic4 + .8*Vic5 + .8*Vic6 + .8*Vic7 + .8*Vic8 + .8*Vic9
        CollSat =~ .8*Sat1 + .8*Sat2 + .8*Sat3 + .8*Sat4 + .8*Sat5
        Persistence =~ .69*graduation_importance + .63*right_decision + .62*will_register + .59*not_graduate + .45*undecided + .44*grades_unimportant
        Anxiety =~ .851*nervous + .887*worry_control + .894*much_worry + 674*cant_relax + .484*restless + .442*irritable + 716*afraid
        Depression =~ .798*anhedonia + .425*down +  .591*sleep +  .913*lo_energy +  .441*appetite +  .519*selfworth +  .755*concentration +  .454*too_slowfast + .695*s_ideation
   
        #Means
         CollegeResponse ~ 2.71*1
         Stigma ~3.61*1
         Victimization ~ 0.11*1
         CollSat ~ 5.61*1
         Persistence ~ 4.41*1
         Anxiety ~ 1.45*1
         Depression ~1.29

         
        #Correlations
         CollegeResponse ~~ .58*Stigma
         CollegeResponse ~~ -.25*Victimization
         CollegeResponse ~~  -.59*CollSat
         CollegeResponse ~~  -.29*Persistence
         CollegeResponse ~~  .17*Anxiety
         CollegeResponse ~~  .18*Depression
         
         Stigma ~~ .37*Victimization
         Stigma ~~  -.41*CollSat
         Stigma ~~  -.19*Persistence
         Stigma ~~  .27*Anxiety
         Stigma ~~  .24*Depression
         
         Victimization ~~  -.22*CollSat
         Victimization ~~  -.04*Persistence
         Victimization ~~  .23*Anxiety
         Victimization ~~  .21*Depression
         
         CollSat ~~  .53*Persistence
         CollSat ~~  -.29*Anxiety
         CollSat ~~  -.32*Depression
         
         Persistence ~~  -.22*Anxiety
         Persistence ~~  -.26*Depression
         
         Anxiety ~~  .76*Depression
        '

set.seed(240218)
dfSzy <- lavaan::simulateData(model = Szymanski_generating_model,
                              model.type = "sem",
                              meanstructure = T,
                              sample.nobs=646,
                              standardized=FALSE)

#used to retrieve column indices used in the rescaling script below
col_index <- as.data.frame(colnames(dfSzy))

#The code below loops through each column of the dataframe and assigns the scaling accordingly
#Rows 1 thru 6 are the Perceptions of LGBTQ Campus Climate Scale
#Rows 7 thru 15 are the Sexual Orientation-Based Campus Victimization Scale
#Rows 16 thru 20 are the College Satisfaction Scale
#Rows 21 thru 26 are the Institutional and Goals Commitment Scale 
#Rows 27 thru 33 are the GAD7
#Rows 34 thru 42 are the PHQ9

for(i in 1:ncol(dfSzy)){  
  if(i >= 1 & i <= 6){   
    dfSzy[,i] <- scales::rescale(dfSzy[,i], c(1, 7))
  }
    if(i >= 7 & i <= 15){   
    dfSzy[,i] <- scales::rescale(dfSzy[,i], c(0, 3))
    }
      if(i >= 16 & i <= 20){  
    dfSzy[,i] <- scales::rescale(dfSzy[,i], c(1, 7))
      }
        if(i >= 21 & i <= 26){  
    dfSzy[,i] <- scales::rescale(dfSzy[,i], c(1, 5))
        }
  if(i >= 27 & i <= 33){  
    dfSzy[,i] <- scales::rescale(dfSzy[,i], c(0, 3))
  }
    if(i >= 34 & i <= 42){  
    dfSzy[,i] <- scales::rescale(dfSzy[,i], c(0, 3))
  }
}

#rounding to integers so that the data resembles that which was collected
library(tidyverse)
dfSzy <- dfSzy %>% round(0) 

#quick check of my work
#psych::describe(dfLewis) 

#Reversing the supportive item on the Perceptions of LGBTQ Campus Climate Scale so that the exercises will be consistent with the format in which the data was collected

dfSzy <- dfSzy %>%
  dplyr::mutate(supportiveNR = 8 - supportive)

#Reversing three items on the Institutional and Goals Commitments scale so that the exercises will be consistent with the format in which the data was collected

dfSzy <- dfSzy %>%
  dplyr::mutate(not_graduateNR = 8 - not_graduate)%>%
  dplyr::mutate(undecidedNR = 8 - undecided)%>%
  dplyr::mutate(grades_unimportantNR = 8 - grades_unimportant)
```

The optional script below will let you save the simulated data to your computing environment as either an .rds object (preserves any formatting you might do)  or a.csv file (think "Excel lite").


```r
# to save the df as an .rds (think 'R object') file on your computer;
# it should save in the same file as the .rmd file you are working
# with saveRDS(SzyDF, 'SzyDF.rds') bring back the simulated dat from
# an .rds file SzyDF <- readRDS('SzyDF.rds')
```


```r
# write the simulated data as a .csv write.table(SzyDF,
# file='SzyDF.csv', sep=',', col.names=TRUE, row.names=FALSE) bring
# back the simulated dat from a .csv file SzyDF <- read.csv
# ('SzyDF.csv', header = TRUE)
```


Although Szymanski and Bissonette report inter-item correlations, it does not appear that they used item analysis to guide their selection of items. In fact, it is not necessary to do so. I teach item analysis because I think it provides a conceptual grounding for future lessons on exploratory and confirmatory factor analysis.

## Steps to Item Analysis

If this is initial scale development, the researchers are wise to write more items than needed so that there is flexibility in selecting items with optimal functioning. Szymaski and Bissonette [-@szymanski_perceptions_2020] do this. Their article narrates how they began with 36 items, narrowed it to 24, and -- on the basis of subject matter expertise and peer review --  further narrowed it to 10. The reduction of additional items happened on the basis of exploratory factor analysis.  

### Step I:  Corrected item-total correlations** 

*A within-scale version of convergent validity.*

* If needed, transform any items (i.e., reverse-coding) and calculate a total score.
* Calculate *corrected item-total correlations* by correlating each item to the total score *excluding* the item being evaluated.
  + to the degree that the item total represents the construct of interest, the items should be strongly correlated with the corrected total score.
* Make decisions about items and scales.  For items that have low or negative correlations
  + consider deletion,
  + consider revision (requires new data collection).
* Each time an item is deleted, the item analysis needs to be repeated because it changes the total-scale score.  
  + In fact, it's a very iterative process. At times, researchers "add back" a previously deleted item (once others are deleted) because with each deletion/addition the statistical construct definition is evolving.
* In multidimensional scales, if the total-scale score is ever used, researchers should conduct item analyses separately for both the total- and the sub- scale scores.
  
There are reasons to not "blindly follow the results of an item analysis" [@green_using_2017].

* **Method factors** (aka *method effects*) are common *methods* that are irrelevant to the characteristics or traits being measured -- yet when analyzed they share variance. Examples of these include negatively word items and common phrasing such as "My supervisor tells me" versus "I receive feedback" [@chyung_evidencebased_2018]. 
* Adequacy of construct representation. That is, how broad is the construct and to what degree do the items represent the entire construct? Threats to the adequacy of the construct representation include:
  + Writing items on a particular, narrow, aspect of the construct, ignoring others.
  + Retaining items that are strongly correlated while deleting those that whose correlations are less strong (although they represent a different aspect of the construct).

This means we should think carefully and simultaneously about:

* statistical properties of the item and overall scale,
* construct definition,
* scale structure (unidimensional?  multidimensional?  hierarchical?).

**Step II:  Correlation of each subscale's items with other subscale totals**

This provides a within-scale version of discriminant validity.

* Calculate scale scores for each of the subscales of a measure.
* Focusing on one subscale at a time, correlate each of the subscale's items with the total scores of all the other subscales.
* Comparing to the results of Step I's corrected item-total process, each item should have stronger correlations with its own items (i.e., the corrected item-total correlation) than with the other subscale total scores.


### Data Prep

Let's do the operational work to get all the pieces we need:

1. Reverse-code the *supportive* variable.
2. From the raw data calculate
   * total-scale score,
   * campus response subscale,
   * stigma subscale.
3. The result is dataset with the item-level data and the three mean scores (total, college response, stigma).

When we review the information about this scale, we learn that the *supportive* item is scaled in the opposite direction of the rest of the items.  That is, a higher score on *supportive* would indicate a positive perception of the campus climate for LGBTQ individuals whereas higher scores on the remaining items indicate a more negative perception. Before moving forward, we must reverse score this item.

In doing this, I will briefly note that in this case I have given my variables one-word names that represent each item. Many researchers (including myself) will often give variable names that are alpha numerical:  LGBTQ1, LGBTQ2, LGBTQ*n*. Either is acceptable. In the psychometrics case, I find the the one-word names to be useful shortcuts as I begin to understand the inter-item relations.

In reverse-scoring the *supportive* item, I will rename it "unsupportive" as an indication of its reversed direction.


```r
dfSzy <- dfSzy %>%
    dplyr::mutate(unsupportive = 8 - supportiveNR)  #scaling 1 to 7; so we subtract from 8

psych::describe(dfSzy)
```

```
                      vars   n mean   sd median trimmed  mad min max range
cold                     1 646 4.11 1.03      4    4.08 1.48   1   7     6
unresponsive             2 646 4.31 0.99      4    4.29 1.48   1   7     6
supportive               3 646 3.69 0.98      4    3.70 1.48   1   7     6
negative                 4 646 3.96 1.04      4    3.98 1.48   1   7     6
heterosexism             5 646 4.00 0.90      4    4.02 1.48   1   7     6
harassed                 6 646 3.91 1.07      4    3.92 1.48   1   7     6
Vic1                     7 646 1.55 0.58      2    1.54 0.00   0   3     3
Vic2                     8 646 1.46 0.54      1    1.45 0.00   0   3     3
Vic3                     9 646 1.50 0.55      2    1.51 1.48   0   3     3
Vic4                    10 646 1.62 0.57      2    1.63 0.00   0   3     3
Vic5                    11 646 1.59 0.54      2    1.61 0.00   0   3     3
Vic6                    12 646 1.41 0.56      1    1.41 0.00   0   3     3
Vic7                    13 646 1.69 0.59      2    1.69 0.00   0   3     3
Vic8                    14 646 1.65 0.56      2    1.66 0.00   0   3     3
Vic9                    15 646 1.46 0.56      1    1.46 0.00   0   3     3
Sat1                    16 646 4.08 1.01      4    4.08 1.48   1   7     6
Sat2                    17 646 4.29 1.04      4    4.26 1.48   1   7     6
Sat3                    18 646 4.44 0.97      4    4.44 1.48   1   7     6
Sat4                    19 646 4.20 1.06      4    4.17 1.48   1   7     6
Sat5                    20 646 4.20 0.94      4    4.20 1.48   1   7     6
graduation_importance   21 646 3.12 0.71      3    3.13 0.00   1   5     4
right_decision          22 646 2.92 0.73      3    2.92 0.00   1   5     4
will_register           23 646 2.90 0.81      3    2.90 1.48   1   5     4
not_graduate            24 646 3.10 0.74      3    3.12 0.00   1   5     4
undecided               25 646 3.09 0.60      3    3.10 0.00   1   5     4
grades_unimportant      26 646 3.04 0.76      3    3.05 0.00   1   5     4
nervous                 27 646 1.57 0.58      2    1.57 0.00   0   3     3
worry_control           28 646 1.48 0.59      1    1.47 1.48   0   3     3
much_worry              29 646 1.53 0.53      2    1.53 0.00   0   3     3
cant_relax              30 646 1.44 0.60      1    1.44 0.00   0   3     3
restless                31 646 1.55 0.58      2    1.54 1.48   0   3     3
irritable               32 646 1.40 0.57      1    1.40 0.00   0   3     3
afraid                  33 646 1.44 0.60      1    1.44 0.00   0   3     3
anhedonia               34 646 1.58 0.58      2    1.59 0.00   0   3     3
down                    35 646 1.56 0.55      2    1.56 0.00   0   3     3
sleep                   36 646 1.64 0.58      2    1.63 0.00   0   3     3
lo_energy               37 646 1.26 0.49      1    1.23 0.00   0   3     3
appetite                38 646 1.40 0.56      1    1.40 0.00   0   3     3
selfworth               39 646 1.57 0.59      2    1.56 0.00   0   3     3
concentration           40 646 1.43 0.61      1    1.43 0.00   0   3     3
too_slowfast            41 646 1.45 0.66      1    1.45 1.48   0   3     3
s_ideation              42 646 1.78 0.46      2    1.83 0.00   0   3     3
supportiveNR            43 646 4.31 0.98      4    4.30 1.48   1   7     6
not_graduateNR          44 646 4.90 0.74      5    4.88 0.00   3   7     4
undecidedNR             45 646 4.91 0.60      5    4.90 0.00   3   7     4
grades_unimportantNR    46 646 4.96 0.76      5    4.95 0.00   3   7     4
unsupportive            47 646 3.69 0.98      4    3.70 1.48   1   7     6
                       skew kurtosis   se
cold                   0.03    -0.17 0.04
unresponsive          -0.10    -0.11 0.04
supportive             0.14     0.40 0.04
negative              -0.18     0.03 0.04
heterosexism          -0.11     0.15 0.04
harassed               0.08     0.04 0.04
Vic1                   0.04    -0.59 0.02
Vic2                   0.08    -0.96 0.02
Vic3                  -0.11    -0.93 0.02
Vic4                  -0.21    -0.42 0.02
Vic5                  -0.23    -0.87 0.02
Vic6                   0.08    -0.69 0.02
Vic7                  -0.21    -0.10 0.02
Vic8                  -0.22    -0.44 0.02
Vic9                   0.05    -0.70 0.02
Sat1                  -0.01    -0.22 0.04
Sat2                   0.00     0.02 0.04
Sat3                  -0.11     0.02 0.04
Sat4                   0.01    -0.29 0.04
Sat5                  -0.08     0.42 0.04
graduation_importance  0.03    -0.02 0.03
right_decision        -0.09    -0.11 0.03
will_register         -0.05    -0.20 0.03
not_graduate          -0.15     0.12 0.03
undecided              0.09     0.37 0.02
grades_unimportant    -0.05    -0.14 0.03
nervous               -0.08    -0.52 0.02
worry_control          0.05    -0.49 0.02
much_worry            -0.02    -1.30 0.02
cant_relax             0.03    -0.41 0.02
restless               0.12    -0.55 0.02
irritable              0.09    -0.51 0.02
afraid                 0.03    -0.41 0.02
anhedonia             -0.22    -0.44 0.02
down                   0.00    -0.91 0.02
sleep                 -0.02    -0.43 0.02
lo_energy              0.51    -0.32 0.02
appetite               0.15    -0.61 0.02
selfworth              0.00    -0.49 0.02
concentration          0.06    -0.33 0.02
too_slowfast           0.11    -0.21 0.03
s_ideation            -0.85     0.27 0.02
supportiveNR          -0.14     0.40 0.04
not_graduateNR         0.15     0.12 0.03
undecidedNR           -0.09     0.37 0.02
grades_unimportantNR   0.05    -0.14 0.03
unsupportive           0.14     0.40 0.04
```

Next, we score the items. In our simulation, we have no missing data. Using an available information approach (AIA; [@parent_handling_2013]) where it is common to allow 20-25% missingness, we might allow the total-scale score to calculate if there is one variable missing. I am inclined to also score the subscales if there is one missing; thus I set the thresshold at 66%. The *mean_n()* function in the *sjstats* packages is especially helpul for this. 


```r
LGBTQvars <- c("cold", "unresponsive", "negative", "heterosexism", "harassed",
    "unsupportive")
ResponseVars <- c("cold", "unresponsive", "unsupportive")
Stigmavars <- c("negative", "heterosexism", "harassed")

dfSzy$Total <- sjstats::mean_n(dfSzy[, LGBTQvars], 0.8)  #will create the mean for each individual if 80% of variables are present (this means there must be at least 5 of 6)
dfSzy$Response <- sjstats::mean_n(dfSzy[, ResponseVars], 0.66)  #will create the mean for each individual if 66% of variables are present (in this case 1 variable can be missing)
dfSzy$Stigma <- sjstats::mean_n(dfSzy[, Stigmavars], 0.66)  #will create the mean for each individual if 66% of variables are present (in this case 1 variable can be missing)

# If the scoring code above does not work for you, try the format
# below which involves inserting to periods in front of the variable
# list. One example is provided. dfLewis$Belonging <-
# sjstats::mean_n(dfLewis[, ..Belonging_vars], 0.80)
```

While we are at it, let's just create tiny dfs with just our variables of interest.

```r
LGBTQ <- dplyr::select(dfSzy, cold, unresponsive, unsupportive, negative,
    heterosexism, harassed)
Response <- dplyr::select(dfSzy, cold, unresponsive, unsupportive)
Stigma <- dplyr::select(dfSzy, negative, heterosexism, harassed)
```


## Calculating Item-Total Correlation Coefficients

Let's first ask, "Is there support for this instrument as a unidimensional measure?"  To do that, we get an alpha for the whole scale score.

The easiest way to do this is apply the *alpha()* function to a tiny df with the variables in that particular scale or subscale. Any variables should be pre-reversed.


```r
LGBTQalpha <- psych::alpha(LGBTQ)  #Although unnecessary, I have saved the output as objects because I will use the objects to create a table 
LGBTQalpha
```

```

Reliability analysis   
Call: psych::alpha(x = LGBTQ)

  raw_alpha std.alpha G6(smc) average_r S/N   ase mean   sd median_r
       0.7       0.7    0.68      0.28 2.4 0.018    4 0.63     0.25

    95% confidence boundaries 
         lower alpha upper
Feldt     0.66   0.7  0.74
Duhachek  0.66   0.7  0.74

 Reliability if an item is dropped:
             raw_alpha std.alpha G6(smc) average_r S/N alpha se  var.r med.r
cold              0.64      0.64    0.61      0.27 1.8    0.022 0.0066  0.22
unresponsive      0.66      0.66    0.63      0.28 2.0    0.021 0.0073  0.25
unsupportive      0.67      0.67    0.63      0.29 2.0    0.021 0.0058  0.25
negative          0.66      0.66    0.63      0.28 2.0    0.021 0.0084  0.25
heterosexism      0.66      0.66    0.63      0.28 2.0    0.021 0.0087  0.25
harassed          0.67      0.67    0.64      0.29 2.0    0.021 0.0078  0.25

 Item statistics 
               n raw.r std.r r.cor r.drop mean   sd
cold         646  0.68  0.68  0.59   0.49  4.1 1.03
unresponsive 646  0.63  0.63  0.51   0.43  4.3 0.99
unsupportive 646  0.62  0.62  0.51   0.42  3.7 0.98
negative     646  0.64  0.63  0.51   0.42  4.0 1.04
heterosexism 646  0.61  0.63  0.51   0.43  4.0 0.90
harassed     646  0.63  0.61  0.49   0.41  3.9 1.07

Non missing response frequency for each item
                1    2    3    4    5    6    7 miss
cold         0.00 0.04 0.22 0.40 0.23 0.09 0.00    0
unresponsive 0.00 0.03 0.17 0.37 0.33 0.09 0.01    0
unsupportive 0.01 0.07 0.35 0.37 0.17 0.02 0.01    0
negative     0.01 0.07 0.23 0.39 0.24 0.05 0.00    0
heterosexism 0.00 0.03 0.24 0.43 0.26 0.03 0.00    0
harassed     0.01 0.07 0.27 0.37 0.22 0.05 0.01    0
```

Examining our list, the overall alpha is 0.70. Further, the average inter-item correlation (*average_r*) is .28.  
*And just hold up a minute, I thought you told us alpha was bad!*  

* While it is less than ideal, we still use it all the time:
  + keeping in mind its relative value (does it increase/decrease, holding other things [like sample size] constant) and
  + examining alpha alternatives (such as we obtained from the omega output)
* Why alpha in this context?  Its information about *consistency* is essential.  In evaluating a scale's reliability we do want to know if items (unidimensionally or across subscales) are responding consistently high/middle/low.

We take note of two columns: 

* *r.cor* is the correlation between the item and the total-scale score with the row-item included. When our focus is on the contribution of a specific item, this information is not helpful since this column gets "extra credit" for the redundancy of the duplicated item.
* *r.drop* is the corrected item-total correlation. This is the better choice because it excludes the row-item being evaluated (eliminating the redundancy) prior to conducting the correlation.
  + Looking at the two columns, notice that the *r.drop* correlations are lower. This is the more honest correlation of the item with the *other* items.
  + In item analysis, we look for items that have relatively high (assessing redundancy or duplication) of items and relatively low (indicating they are unlike the other items) values. 
  
If we thought an item was problematic, we could eliminate it and rerun the analysis. Because we are looking at a list of items that "made the cut," we don't have any items that are concerningly high or low. For demonstration purposes, though, the corrected item-total correlation (*r.drop*) of the *harassed* variable was the lowest (0.40). Let's re-run the analysis excluding this item.


```r
minus_harassed <- dplyr::select(dfSzy, cold, unresponsive, unsupportive,
    negative, heterosexism)
```


```r
psych::alpha(minus_harassed)
```

```

Reliability analysis   
Call: psych::alpha(x = minus_harassed)

  raw_alpha std.alpha G6(smc) average_r S/N   ase mean   sd median_r
      0.67      0.67    0.64      0.29   2 0.021    4 0.65     0.25

    95% confidence boundaries 
         lower alpha upper
Feldt     0.63  0.67  0.71
Duhachek  0.63  0.67  0.71

 Reliability if an item is dropped:
             raw_alpha std.alpha G6(smc) average_r S/N alpha se  var.r med.r
cold              0.58      0.58    0.53      0.26 1.4    0.027 0.0060  0.22
unresponsive      0.62      0.62    0.56      0.29 1.6    0.025 0.0079  0.25
unsupportive      0.61      0.61    0.56      0.28 1.6    0.025 0.0072  0.25
negative          0.65      0.64    0.58      0.31 1.8    0.022 0.0093  0.30
heterosexism      0.64      0.64    0.58      0.31 1.8    0.023 0.0097  0.30

 Item statistics 
               n raw.r std.r r.cor r.drop mean   sd
cold         646  0.72  0.71  0.61   0.50  4.1 1.03
unresponsive 646  0.66  0.66  0.53   0.43  4.3 0.99
unsupportive 646  0.67  0.67  0.55   0.45  3.7 0.98
negative     646  0.63  0.62  0.46   0.37  4.0 1.04
heterosexism 646  0.60  0.62  0.47   0.38  4.0 0.90

Non missing response frequency for each item
                1    2    3    4    5    6    7 miss
cold         0.00 0.04 0.22 0.40 0.23 0.09 0.00    0
unresponsive 0.00 0.03 0.17 0.37 0.33 0.09 0.01    0
unsupportive 0.01 0.07 0.35 0.37 0.17 0.02 0.01    0
negative     0.01 0.07 0.23 0.39 0.24 0.05 0.00    0
heterosexism 0.00 0.03 0.24 0.43 0.26 0.03 0.00    0
```

The alpha $(\alpha = 0.67)$ decreases; the overall inter-item correlations increase, slightly (*average_r*; 0.29). This decrease in alpha is an example of how sample size can effect the result.

Examining item-level statistics, we do see greater variability (0.37 to 0.50) in the corrected item-total correlations (*r.drop*).  What might this mean?  

* The item we dropped (*harassed*) may be clustering with *negative* and *heterosexism* in a subordinate factor (think subscale).
* Although item analysis is more of a tool in assessing reliability, the statistical information that *harassed* provided may broaden the construct definition (definitions are a concern of *validity*) of perceptions of campus climate such that it is necessary to ground/anchor *negative* and *heterosexism*.

Tentative conclusion: there is evidence that this is not a unidimensional measure. Let's move on to inspect similar data for each of the subscales. We'll start with the College Response subscale.


```r
RESPalpha <- psych::alpha(Response)
RESPalpha
```

```

Reliability analysis   
Call: psych::alpha(x = Response)

  raw_alpha std.alpha G6(smc) average_r S/N   ase mean   sd median_r
      0.66      0.66    0.57      0.39 1.9 0.023    4 0.77      0.4

    95% confidence boundaries 
         lower alpha upper
Feldt     0.61  0.66  0.70
Duhachek  0.62  0.66  0.71

 Reliability if an item is dropped:
             raw_alpha std.alpha G6(smc) average_r S/N alpha se var.r med.r
cold              0.52      0.52    0.35      0.35 1.1    0.038    NA  0.35
unresponsive      0.60      0.60    0.42      0.42 1.5    0.032    NA  0.42
unsupportive      0.58      0.58    0.40      0.40 1.4    0.033    NA  0.40

 Item statistics 
               n raw.r std.r r.cor r.drop mean   sd
cold         646  0.80  0.79  0.62   0.50  4.1 1.03
unresponsive 646  0.76  0.76  0.55   0.45  4.3 0.99
unsupportive 646  0.76  0.77  0.57   0.46  3.7 0.98

Non missing response frequency for each item
                1    2    3    4    5    6    7 miss
cold         0.00 0.04 0.22 0.40 0.23 0.09 0.00    0
unresponsive 0.00 0.03 0.17 0.37 0.33 0.09 0.01    0
unsupportive 0.01 0.07 0.35 0.37 0.17 0.02 0.01    0
```

The alpha for the College Response subscale is 0.66; this is a bit lower than the alpha for the total scale score $(\alpha = 0.70)$. The average inter-item correlation (*average_r*) is higher somewhat higher than the that of the total scale score (0.39 versus 0.28). 

Examining the corrected item-total correlations (r.drop) indicates strong correlations between the row-item with the remaining variables (0.45 to 0.50).

Let's examine at the Stigma subscale.


```r
STIGalpha <- psych::alpha(Stigma)
STIGalpha
```

```

Reliability analysis   
Call: psych::alpha(x = Stigma)

  raw_alpha std.alpha G6(smc) average_r S/N   ase mean   sd median_r
      0.62      0.63    0.53      0.36 1.7 0.025    4 0.76     0.36

    95% confidence boundaries 
         lower alpha upper
Feldt     0.57  0.62  0.67
Duhachek  0.57  0.62  0.67

 Reliability if an item is dropped:
             raw_alpha std.alpha G6(smc) average_r S/N alpha se var.r med.r
negative          0.52      0.52    0.35      0.35 1.1    0.038    NA  0.35
heterosexism      0.53      0.53    0.36      0.36 1.1    0.037    NA  0.36
harassed          0.53      0.54    0.37      0.37 1.2    0.036    NA  0.37

 Item statistics 
               n raw.r std.r r.cor r.drop mean  sd
negative     646  0.77  0.76  0.56   0.44  4.0 1.0
heterosexism 646  0.73  0.76  0.55   0.44  4.0 0.9
harassed     646  0.77  0.75  0.54   0.43  3.9 1.1

Non missing response frequency for each item
                1    2    3    4    5    6    7 miss
negative     0.01 0.07 0.23 0.39 0.24 0.05 0.00    0
heterosexism 0.00 0.03 0.24 0.43 0.26 0.03 0.00    0
harassed     0.01 0.07 0.27 0.37 0.22 0.05 0.01    0
```

The alpha for the Stigma subscale is 0.63; this is a bit lower than the alpha for the total-scale $(\alpha = 0.70)$. In contrast, the inter-item correlation (*average_r*) is a bit higher than the same for the total scale score (0.36 versus 0.28). 

Examining the corrected item-total correlations (r.drop) indicates a strong correlation between the row-item with the remaining variables (0.43 to 0.44).

In addition to needing strong inter-item correlations (which we just assessed) we want the individual items to correlate more strongly with themselves than with the other scale. Let's do that next.

## Correlating Items with Other Scale Totals

In this first analysis, we will correlate the individual *items* from the College Response subscale to the Stigma subscale *score.*


```r
apaTables::apa.cor.table(dfSzy[c("cold", "unresponsive", "unsupportive",
    "Stigma")])
```

```


Means, standard deviations, and correlations with confidence intervals
 

  Variable        M    SD   1          2          3         
  1. cold         4.11 1.03                                 
                                                            
  2. unresponsive 4.31 0.99 .40**                           
                            [.34, .47]                      
                                                            
  3. unsupportive 3.69 0.98 .42**      .35**                
                            [.36, .49] [.28, .42]           
                                                            
  4. Stigma       3.96 0.76 .33**      .28**      .26**     
                            [.26, .39] [.21, .35] [.18, .33]
                                                            

Note. M and SD are used to represent mean and standard deviation, respectively.
Values in square brackets indicate the 95% confidence interval.
The confidence interval is a plausible range of population correlations 
that could have caused the sample correlation (Cumming, 2014).
 * indicates p < .05. ** indicates p < .01.
 
```
We want the corrected item-total correlations of the College Response scale (0.45 to 0.50; retrieved from the *r.drop* column above)to be higher than their correlations with the Stigma scale (0.28 to 0.33) with all three items). These items follow the pattern.

Let's examine the individual items from the Stigma scale with the College Response subscale score.


```r
apaTables::apa.cor.table(dfSzy[c("negative", "heterosexism", "harassed",
    "Response")])
```

```


Means, standard deviations, and correlations with confidence intervals
 

  Variable        M    SD   1          2          3         
  1. negative     3.96 1.04                                 
                                                            
  2. heterosexism 4.00 0.90 .37**                           
                            [.30, .43]                      
                                                            
  3. harassed     3.91 1.07 .36**      .35**                
                            [.29, .42] [.28, .42]           
                                                            
  4. Response     4.04 0.77 .29**      .29**      .27**     
                            [.22, .36] [.22, .36] [.20, .34]
                                                            

Note. M and SD are used to represent mean and standard deviation, respectively.
Values in square brackets indicate the 95% confidence interval.
The confidence interval is a plausible range of population correlations 
that could have caused the sample correlation (Cumming, 2014).
 * indicates p < .05. ** indicates p < .01.
 
```

Similarly, the corrected item-total correlations (i.e., *r.drop*) from the Stigma subscale  (0.43 to 0.44) are stronger than their correlation with the College Response subsale (0.27 to 0.29).

## Interpreting and Writing up the Results

Tabling these results can be really useful to present them effectively. As is customary in APA style tables, when the item is in bold, the value represents its relationship with its own factor. These values come from the corrected item-total (*r.drop*) values where the item is singled out and correlated with the remaining items in its subscale.

|Item-Total Correlations of Items with their Own and Other Subscales
|:-------------------------------------|

|Variables     |College Response |Stigma
|:-------------|:---------:|:---------:|
|cold          |**.50**    |0.33       |
|unresponsive  |**.45**    |0.28       |
|unsupportive  |**.46**    |0.26       |
|negative      |0.29       |**0.44**    |
|heterosexism  |0.29       |**0.44**    |
|harassed      |0.27       |**0.43**    |

Although I pitched this type of item-analysis as *reliability*, to some degree it assesses within-scale **convergent and discriminant validity** because we can see the item relates more strongly to members of its own scale (higher correlation coefficients indicate *convergence*) than to the subscale scores of the other scales. When this pattern occurs, we can argue that the items *discriminate* well.

**Results**

Item analyses were conducted on the six items hypothesized to assess perceptions of campus climate for members of the LGBTQ community. To assess the within-scale convergent and discrimninant validity of the College Response and Stigma subscales, each item was correlated with its own scale (with the item removed) and with the other coping scale (see Table 1). In all cases, items were more highly correlated with their own scale than with the other scale. Coefficient alphas were 0.66, 0.63, and 0.70 for the College Response, Stigma, and total-scale scores, respectively. We concluded that the within-scale convergent and discriminant validity of this measure is strong.

For your consideration:
You are at your dissertation defense.  For one of your measures, the Cronbach’s alpha is .45.  A committee member asks, “So why was the alpha coefficient so low?”  On the basis of what you have learned in this lesson, how do you respond?

## A Conversation with Dr. Szymanski

Doctoral students Julian Williams (Industrial-Organizational Psychology), Jaylee York (Clinical Psychology), and I  were able to interview the first author (Dawn Szymanski, PhD) about the article [@szymanski_perceptions_2020] and what it means. Here's a direct [link](https://spu.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=0f9696ab-df9a-452b-8ccd-aee101271054) to that interview.

Among other things, we asked:

* How were you able to create such an efficient (6 items) survey?
* What were the decisions around a potential third factor of *visibility*?
* What would you say to senior leadership on a college campus (where there hiring policies that discriminate against LGBTQIA+ applicants) who will acknowledge the research that indicates that the existence of such policies are associated with reduced well-being for members of the LGBTQIA+ community but who insists that their campus is different?
* How would you like to see the article used?

## Practice Problems
   
In each of these lessons I provide suggestions for practice that allow you to select one or more problems that are graded in difficulty. For this lesson, please locate item-level data for a scale that has the potential for at least two subscales  and a total-scale score. Ideally, you selected such data for practice from the prior lesson. Then, please examine the following:

* produce alpha coefficients, average inter-item correlations, and corrected item-total correlations for the total and subscales, separately
* produce correlations between the individual items of one subscale and the subscale scores of all other scales
* draft an APA style results section with an accompanying table.

In my example, there were only two subscales. If you have more, you will need to compare each subscale with all the others. For example, if you had three subscales:  A, B, C, you would need to compare A/B, B/C, and A/C.

### Problem #1:  Play around with this simulation.

Copy the script for the simulation and then change (at least) one thing in the simulation to see how it impacts the results.  

If item analysis is new to you, copy the script for the simulation and then change (at least) one thing in the simulation to see how it impacts the results. Perhaps you just change the number in "set.seed(210827)" from 210827 to something else. Your results should parallel those obtained in the lecture, making it easier for you to check your work as you go. 

### Problem #2: Use raw data from the ReCentering Psych Stats survey on Qualtrics.

The script below pulls live data directly from the ReCentering Psych Stats survey on Qualtrics. As described in the [Scrubbing and Scoring chapters](https://lhbikos.github.io/ReC_MultivariateModeling/) of the ReCentering Psych Stats Multivariate Modeling volume, the Perceptions of the LGBTQ College Campus Climate Scale [@szymanski_perceptions_2020] was included (LGBTQ) and further adapted to assess perceptions of campus climate for Black students (BLst), non-Black students of color (nBSoC), international students (INTst), and students with disabilities (wDIS). Consider conducting the analyses on one of these scales or merging them together and imagining subscales according to identity/group (LGBTQ, Black, non-Black, disability, international) or College Response and Stigma across the different groups.


```r
library(tidyverse)
# only have to run this ONCE to draw from the same Qualtrics
# account...but will need to get different token if you are changing
# between accounts
library(qualtRics)
# qualtrics_api_credentials(api_key =
# 'mUgPMySYkiWpMFkwHale1QE5HNmh5LRUaA8d9PDg', base_url =
# 'spupsych.az1.qualtrics.com', overwrite = TRUE, install = TRUE)
QTRX_df <- qualtRics::fetch_survey(surveyID = "SV_b2cClqAlLGQ6nLU", time_zone = NULL,
    verbose = FALSE, label = FALSE, convert = FALSE, force_request = TRUE,
    import_id = FALSE)
climate_df <- QTRX_df %>%
    select("Blst_1", "Blst_2", "Blst_3", "Blst_4", "Blst_5", "Blst_6",
        "nBSoC_1", "nBSoC_2", "nBSoC_3", "nBSoC_4", "nBSoC_5", "nBSoC_6",
        "INTst_1", "INTst_2", "INTst_3", "INTst_4", "INTst_5", "INTst_6",
        "wDIS_1", "wDIS_2", "wDIS_3", "wDIS_4", "wDIS_5", "wDIS_6", "LGBTQ_1",
        "LGBTQ_2", "LGBTQ_3", "LGBTQ_4", "LGBTQ_5", "LGBTQ_6")
# Item numbers are supported with the following items: _1 'My campus
# unit provides a supportive environment for ___ students' _2
# '________ is visible in my campus unit' _3 'Negative attitudes
# toward persons who are ____ are openly expressed in my campus
# unit.' _4 'My campus unit is unresponsive to the needs of ____
# students.' _5 'Students who are_____ are harassed in my campus
# unit.' _6 'My campus unit is cold and uncaring toward ____
# students.'

# Item 1 on each subscale should be reverse coded. The College
# Response scale is composed of items 1, 4, 6, The Stigma scale is
# composed of items 2,3, 5
```


The optional script below will let you save the simulated data to your computing environment as either a .csv file (think "Excel lite") or .rds object (preserves any formatting you might do).

```r
# write the simulated data as a .csv write.table(climate_df,
# file='climate_df.csv', sep=',', col.names=TRUE, row.names=FALSE)
# bring back the simulated dat from a .csv file climate_df <-
# read.csv ('climate_df.csv', header = TRUE)
```


```r
# to save the df as an .rds (think 'R object') file on your computer;
# it should save in the same file as the .rmd file you are working
# with saveRDS(climate_df, 'climate_df.rds') bring back the simulated
# dat from an .rds file climate_df <- readRDS('climate_df.rds')
```

### Problem #3:  Try something entirely new.

Complete the same steps using data for which you have permission and access.  This might be data of your own, from your lab, simulated from an article, or located on an open repository.

### Grading Rubric

Using the lecture and workflow (chart) as a guide, please work through all the steps listed in the proposed assignment/grading rubric.

|Assignment Component                    | Points Possible   | Points Earned|
|:-------------------------------------- |:----------------: |:------------:|
|1. Check and, if needed, format and score data |      5            |_____  |           
|2. Report alpha coefficients and average inter-item correlations for the total and subscales|5  |_____  |
|3. Produce and interpret corrected item-total correlations for total and subscales, separately|5| _____  |  
|4. Produce and interpret correlations between the individual items of a given subscale and the subscale scores of all other subscales| 5 |_____  |               
|5. APA style results section with table        |    5        |_____  |   
|6. Explanation to grader                 |    5        |_____  |       
|**Totals**                               |      30       |_____  |           


## Bonus Reel: 

![Image of a filmstrip](images/film-strip-1.jpg)

For our interpretation and results, I created the table by manually typing in the results. Since there were only two subscales, this was easy. However, it can be a very useful skill (and prevent typing errors) by leveraging R's capabilities to build a table.

The script below

* Creates a correlation matrix of the items of each scale and correlates them with the "other" subscale, separately for both subscales.
* Extracts the r.drop from each subscale
* Joins (adds more variables) the analyses across the corrected item-total and item-other subscale analyses
* Binds (adds more cases) the two sets of items together


```r
Resp_othR <- psych::corr.test(dfSzy[c("negative", "heterosexism", "harassed",
    "Response")])  #Run the correlation of the subscale and the items that are *not* on the subscale
Resp_othR <- as.data.frame(Resp_othR$r)  #extracts the 'r' matrix and makes it a df
Resp_othR$Items <- c("negative", "heterosexism", "harassed", "Response")  #Assigning names to the items
Resp_othR <- Resp_othR[!Resp_othR$Items == "Response", ]  #Removing the subscale score as a a row in the df
Resp_othR[, "Stigma"] <- NA  #We need a column for this to bind the items later
Resp_othR <- dplyr::select(Resp_othR, Items, Response, Stigma)  #All we need is the item name and the correlations with the subscales
RESPalpha <- as.data.frame(RESPalpha$item.stats)  #Grabbing the alpha objet we created earlier and making it a df  
RESPalpha$Items <- c("cold", "unresponsive", "unsupportive")

Stig_othR <- psych::corr.test(dfSzy[c("cold", "unresponsive", "unsupportive",
    "Stigma")])  #Run the correlation of the subscale and the items that are *not* on the subscale
Stig_othR <- as.data.frame(Stig_othR$r)  #extracts the 'r' matrix and makes it a df
Stig_othR$Items <- c("cold", "unresponsive", "unsupportive", "Stigma")  #Assigning names to the items
Stig_othR <- Stig_othR[!Stig_othR$Items == "Stigma", ]  #Removing the subscale score as a a row in the df
Stig_othR[, "Response"] <- NA  #We need a column for this to bind the items later
Stig_othR <- dplyr::select(Stig_othR, Items, Response, Stigma)  #All we need is the item name and the correlations with the subscales
STIGalpha <- as.data.frame(STIGalpha$item.stats)  #Grabbing the alpha objet we created earlier and making it a df  
STIGalpha$Items <- c("negative", "heterosexism", "harassed")

# Combining these four dfs
ResponseStats <- full_join(RESPalpha, Stig_othR, by = "Items")
ResponseStats$Response <- ResponseStats$r.drop
ResponseStats <- dplyr::select(ResponseStats, Items, Response, Stigma)
StigmaStats <- full_join(STIGalpha, Resp_othR, by = "Items")
StigmaStats$Stigma <- StigmaStats$r.drop
StigmaStats <- dplyr::select(StigmaStats, Items, Response, Stigma)
ItemAnalyses <- rbind(ResponseStats, StigmaStats)
ItemAnalyses
```

```
         Items  Response    Stigma
1         cold 0.5041391 0.3258401
2 unresponsive 0.4490390 0.2783617
3 unsupportive 0.4644473 0.2581391
4     negative 0.2874243 0.4401670
5 heterosexism 0.2925477 0.4365623
6     harassed 0.2704033 0.4291150
```

```r
# Writing them to a .csv file allows post-r formatting
write.csv(ItemAnalyses, file = "LGBTQ_Climate_ItemAnalyses.csv", sep = ",",
    row.names = TRUE, col.names = TRUE)
```









## Homeworked Example
[Screencast Link](link)

For more information about the data used in this homeworked example, please refer to the description and codebook located at the end of the [introduction](ReCintro) in first volume of ReCentering Psych Stats.

As a brief review, this data is part of an IRB-approved study, with consent to use in teaching demonstrations and to be made available to the general public via the open science framework. Hence, it is appropriate to share in class.  You will notice there are student- and teacher- IDs. These numbers are not connected to the SPU student ID. Rather, the subcontractor who does the course evals for SPU creates a third, not-SPU-related identifier.

This is the same dataset I have been using for many in-class demos. It's great for psychometrics because I actually used some of our Canvas course items in the three dimensions/factors. We'll get to walk through that process in this class.

Because this is an actual dataset, if you wish to work the problem along with me, you will need to download the data from **LINK TO DATASET**.

In this example, my concern is an item analysis with the items from the three subscales (i.e., valued-by-the-student, traditional pedagogy, socially responsive pedagogy) that I created from the course evaluation items used at my institution.

### Check and, if needed, format and score data 	


```r
big <- readRDS("ReC.rds")
```

With the next code I will create an item-level df with only the items used in the three scales. 


```r
library(tidyverse)
items <- big%>%
  dplyr::select (ValObjectives, IncrUnderstanding, IncrInterest, ClearResponsibilities, EffectiveAnswers, Feedback, ClearOrganization, ClearPresentation, MultPerspectives, InclusvClassrm, DEIintegration,EquitableEval)
```

Next I check the structure of the data.


```r
str(items)
```

```
Classes 'data.table' and 'data.frame':	310 obs. of  12 variables:
 $ ValObjectives        : int  5 5 4 4 5 5 5 5 4 5 ...
 $ IncrUnderstanding    : int  2 3 4 3 4 4 5 2 4 5 ...
 $ IncrInterest         : int  5 3 4 2 4 3 5 3 2 5 ...
 $ ClearResponsibilities: int  5 5 4 4 5 4 5 4 4 5 ...
 $ EffectiveAnswers     : int  5 3 5 3 5 3 4 3 2 3 ...
 $ Feedback             : int  5 3 4 2 5 NA 5 4 4 5 ...
 $ ClearOrganization    : int  3 4 3 4 4 4 5 4 4 5 ...
 $ ClearPresentation    : int  4 4 4 2 5 3 4 4 4 5 ...
 $ MultPerspectives     : int  5 5 4 5 5 4 5 5 5 5 ...
 $ InclusvClassrm       : int  5 5 5 5 5 4 5 5 4 5 ...
 $ DEIintegration       : int  5 5 5 5 5 4 5 5 5 5 ...
 $ EquitableEval        : int  5 5 3 5 5 3 5 5 3 5 ...
 - attr(*, ".internal.selfref")=<externalptr> 
```

### Report alpha coefficients and average inter-item correlations for the total and subscales

This task is completed in the next section.

### Produce and interpret corrected item-total correlations for total and subscales, separately

In the lecture, I created baby dfs of the subscales and ran the alphas on those; another option is to create lists of variables (i.e., variable vectors) and use that instead. We can later use those same variable vectors to score the items.

#### All Course Evaluation Items

First, I will calculate the alpha coefficient and inter-item correlations for the total score representing the course evaluation items.


```r
psych::alpha(items)
```

```

Reliability analysis   
Call: psych::alpha(x = items)

  raw_alpha std.alpha G6(smc) average_r S/N    ase mean   sd median_r
      0.92      0.92    0.93      0.49  11 0.0065  4.3 0.61     0.48

    95% confidence boundaries 
         lower alpha upper
Feldt     0.90  0.92  0.93
Duhachek  0.91  0.92  0.93

 Reliability if an item is dropped:
                      raw_alpha std.alpha G6(smc) average_r  S/N alpha se var.r
ValObjectives              0.92      0.92    0.93      0.51 11.3   0.0067 0.016
IncrUnderstanding          0.91      0.91    0.92      0.49 10.6   0.0070 0.016
IncrInterest               0.91      0.91    0.92      0.49 10.4   0.0070 0.018
ClearResponsibilities      0.91      0.91    0.92      0.48 10.0   0.0073 0.015
EffectiveAnswers           0.91      0.91    0.92      0.48 10.0   0.0074 0.016
Feedback                   0.91      0.91    0.92      0.48 10.3   0.0071 0.018
ClearOrganization          0.91      0.91    0.92      0.48 10.2   0.0073 0.016
ClearPresentation          0.91      0.91    0.92      0.47  9.7   0.0076 0.015
MultPerspectives           0.91      0.91    0.92      0.48 10.0   0.0073 0.017
InclusvClassrm             0.91      0.91    0.92      0.49 10.6   0.0069 0.018
DEIintegration             0.92      0.92    0.93      0.52 11.8   0.0063 0.011
EquitableEval              0.91      0.91    0.93      0.49 10.5   0.0070 0.018
                      med.r
ValObjectives          0.53
IncrUnderstanding      0.50
IncrInterest           0.48
ClearResponsibilities  0.48
EffectiveAnswers       0.48
Feedback               0.48
ClearOrganization      0.48
ClearPresentation      0.47
MultPerspectives       0.47
InclusvClassrm         0.52
DEIintegration         0.53
EquitableEval          0.48

 Item statistics 
                        n raw.r std.r r.cor r.drop mean   sd
ValObjectives         309  0.59  0.61  0.55   0.53  4.5 0.61
IncrUnderstanding     309  0.71  0.70  0.67   0.64  4.3 0.82
IncrInterest          308  0.75  0.73  0.71   0.68  3.9 0.99
ClearResponsibilities 307  0.80  0.80  0.79   0.75  4.4 0.82
EffectiveAnswers      308  0.80  0.79  0.78   0.75  4.4 0.83
Feedback              304  0.75  0.75  0.72   0.69  4.2 0.88
ClearOrganization     309  0.79  0.77  0.75   0.72  4.0 1.08
ClearPresentation     309  0.85  0.84  0.83   0.80  4.2 0.92
MultPerspectives      305  0.79  0.80  0.78   0.75  4.4 0.84
InclusvClassrm        301  0.68  0.70  0.67   0.62  4.6 0.68
DEIintegration        273  0.51  0.53  0.49   0.42  4.5 0.74
EquitableEval         308  0.70  0.72  0.69   0.66  4.6 0.63

Non missing response frequency for each item
                         1    2    3    4    5 miss
ValObjectives         0.00 0.01 0.03 0.39 0.57 0.00
IncrUnderstanding     0.01 0.04 0.07 0.44 0.45 0.00
IncrInterest          0.02 0.09 0.14 0.44 0.31 0.01
ClearResponsibilities 0.01 0.02 0.07 0.31 0.59 0.01
EffectiveAnswers      0.01 0.02 0.08 0.36 0.53 0.01
Feedback              0.01 0.05 0.10 0.39 0.46 0.02
ClearOrganization     0.04 0.07 0.10 0.41 0.38 0.00
ClearPresentation     0.02 0.05 0.07 0.40 0.46 0.00
MultPerspectives      0.02 0.02 0.08 0.33 0.56 0.02
InclusvClassrm        0.01 0.01 0.05 0.23 0.70 0.03
DEIintegration        0.00 0.01 0.10 0.22 0.67 0.12
EquitableEval         0.00 0.01 0.03 0.32 0.63 0.01
```
At the total scale level, $\alpha = 0.92$; the average inter-item correlations are 0.487; and the corrected item-total correlations (*r.drop*) range from 0.55 to 0.83.

To obtain this data at the subscale level I will first create variable vectors.


```r
Valued_vars <- c('ValObjectives', 'IncrUnderstanding', 'IncrInterest')
TradPed_vars <- c('ClearResponsibilities', 'EffectiveAnswers', 'Feedback', 'ClearOrganization', 'ClearPresentation')
SCRPed_vars <- c('MultPerspectives', 'InclusvClassrm', 'DEIintegration','EquitableEval')
```

I can insert these variable vectors into the *psych::alpha()* function to obtain the information.

#### Valued-by-Student Subscale


```r
psych::alpha(items[,Valued_vars])
```

```

Reliability analysis   
Call: psych::alpha(x = items[, Valued_vars])

  raw_alpha std.alpha G6(smc) average_r S/N  ase mean   sd median_r
      0.77      0.77    0.71      0.53 3.4 0.02  4.2 0.68     0.48

    95% confidence boundaries 
         lower alpha upper
Feldt     0.72  0.77  0.81
Duhachek  0.73  0.77  0.81

 Reliability if an item is dropped:
                  raw_alpha std.alpha G6(smc) average_r S/N alpha se var.r
ValObjectives          0.80      0.81    0.68      0.68 4.3    0.022    NA
IncrUnderstanding      0.60      0.65    0.48      0.48 1.8    0.040    NA
IncrInterest           0.59      0.61    0.44      0.44 1.6    0.044    NA
                  med.r
ValObjectives      0.68
IncrUnderstanding  0.48
IncrInterest       0.44

 Item statistics 
                    n raw.r std.r r.cor r.drop mean   sd
ValObjectives     309  0.71  0.77  0.55   0.50  4.5 0.61
IncrUnderstanding 309  0.86  0.85  0.76   0.68  4.3 0.82
IncrInterest      308  0.90  0.87  0.79   0.70  3.9 0.99

Non missing response frequency for each item
                     1    2    3    4    5 miss
ValObjectives     0.00 0.01 0.03 0.39 0.57 0.00
IncrUnderstanding 0.01 0.04 0.07 0.44 0.45 0.00
IncrInterest      0.02 0.09 0.14 0.44 0.31 0.01
```

The alpha for Valued-by-the-Student subscale is 0.77.  I will start building my homework table as I go along by adding the corrected item-total correlations (i.e., the *r.drop*) column.

|Item-Total Correlations of Items with their Own and Other Subscales
|:------------------------------------------------------|

|Variables             |Valued    |TradPed   |SCRPed    |
|:---------------------|:--------:|:--------:|:--------:|
|ValObjectives         |**.50**   |          |          |
|IncrUnderstanding     |**.68**   |          |          |
|IncrInterest          |**.70**   |          |          |
|ClearResponsibilities |          |          |          |
|EffectiveAnswers      |          |          |          |
|Feedback              |          |          |          |
|ClearOrganization     |          |          |          |
|ClearPresentation     |          |          |          |
|MultPerspectives      |          |          |          |
|DEIintegration        |          |          |          |
|EquitableEval         |          |          |          |
|Feedback              |          |          |          |

#### Traditional Pedagogy Items

Next I will produce the output for the Traditional Pedagogy subscale.

```r
psych::alpha(items[,TradPed_vars])
```

```

Reliability analysis   
Call: psych::alpha(x = items[, TradPed_vars])

  raw_alpha std.alpha G6(smc) average_r S/N    ase mean   sd median_r
      0.89       0.9    0.88      0.64 8.8 0.0094  4.3 0.76     0.65

    95% confidence boundaries 
         lower alpha upper
Feldt     0.87  0.89  0.91
Duhachek  0.88  0.89  0.91

 Reliability if an item is dropped:
                      raw_alpha std.alpha G6(smc) average_r S/N alpha se  var.r
ClearResponsibilities      0.86      0.86    0.84      0.62 6.4    0.013 0.0054
EffectiveAnswers           0.87      0.87    0.84      0.63 6.8    0.012 0.0045
Feedback                   0.89      0.89    0.87      0.68 8.4    0.010 0.0016
ClearOrganization          0.88      0.88    0.85      0.64 7.2    0.012 0.0044
ClearPresentation          0.86      0.87    0.83      0.62 6.5    0.013 0.0030
                      med.r
ClearResponsibilities  0.59
EffectiveAnswers       0.65
Feedback               0.69
ClearOrganization      0.66
ClearPresentation      0.62

 Item statistics 
                        n raw.r std.r r.cor r.drop mean   sd
ClearResponsibilities 307  0.87  0.87  0.84   0.79  4.4 0.82
EffectiveAnswers      308  0.84  0.85  0.81   0.76  4.4 0.83
Feedback              304  0.78  0.79  0.70   0.66  4.2 0.88
ClearOrganization     309  0.85  0.83  0.78   0.74  4.0 1.08
ClearPresentation     309  0.87  0.87  0.83   0.78  4.2 0.92

Non missing response frequency for each item
                         1    2    3    4    5 miss
ClearResponsibilities 0.01 0.02 0.07 0.31 0.59 0.01
EffectiveAnswers      0.01 0.02 0.08 0.36 0.53 0.01
Feedback              0.01 0.05 0.10 0.39 0.46 0.02
ClearOrganization     0.04 0.07 0.10 0.41 0.38 0.00
ClearPresentation     0.02 0.05 0.07 0.40 0.46 0.00
```

Traditional Pedagogy $\alpha = 0.90$. I retrieve the corrected item-total correlations from the *r.drop* column.

|Item-Total Correlations of Items with their Own and Other Subscales
|:------------------------------------------------------|

|Variables             |Valued    |TradPed   |SCRPed    |
|:---------------------|:--------:|:--------:|:--------:|
|ValObjectives         |**.50**   |          |          |
|IncrUnderstanding     |**.67**   |          |          |
|IncrInterest          |**.70**   |          |          |
|ClearResponsibilities |          |**.79**   |          |
|EffectiveAnswers      |          |**.76**   |          |
|Feedback              |          |**.66**   |          |
|ClearOrganization     |          |**.74**   |          |
|ClearPresentation     |          |**.78**   |          |
|MultPerspectives      |          |          |          |
|DEIintegration        |          |          |          |
|EquitableEval         |          |          |          |
|Feedback              |          |          |          |


#### Socially Responsive Pedagogy Items


```r
psych::alpha(items[,SCRPed_vars])
```

```

Reliability analysis   
Call: psych::alpha(x = items[, SCRPed_vars])

  raw_alpha std.alpha G6(smc) average_r S/N   ase mean   sd median_r
      0.81      0.81    0.78      0.52 4.3 0.017  4.5 0.58     0.54

    95% confidence boundaries 
         lower alpha upper
Feldt     0.77  0.81  0.84
Duhachek  0.77  0.81  0.84

 Reliability if an item is dropped:
                 raw_alpha std.alpha G6(smc) average_r S/N alpha se  var.r
MultPerspectives      0.73      0.74    0.67      0.49 2.8    0.026 0.0153
InclusvClassrm        0.74      0.74    0.67      0.49 2.9    0.025 0.0120
DEIintegration        0.78      0.78    0.71      0.54 3.6    0.021 0.0044
EquitableEval         0.78      0.79    0.73      0.56 3.9    0.021 0.0034
                 med.r
MultPerspectives  0.47
InclusvClassrm    0.50
DEIintegration    0.57
EquitableEval     0.57

 Item statistics 
                   n raw.r std.r r.cor r.drop mean   sd
MultPerspectives 305  0.85  0.83  0.76   0.68  4.4 0.84
InclusvClassrm   301  0.82  0.83  0.76   0.67  4.6 0.68
DEIintegration   273  0.78  0.78  0.67   0.59  4.5 0.74
EquitableEval    308  0.75  0.76  0.64   0.58  4.6 0.63

Non missing response frequency for each item
                    1    2    3    4    5 miss
MultPerspectives 0.02 0.02 0.08 0.33 0.56 0.02
InclusvClassrm   0.01 0.01 0.05 0.23 0.70 0.03
DEIintegration   0.00 0.01 0.10 0.22 0.67 0.12
EquitableEval    0.00 0.01 0.03 0.32 0.63 0.01
```

Alpha for the SCR Pedagogy dimension is .81

|Item-Total Correlations of Items with their Own and Other Subscales
|:------------------------------------------------------|

|Variables             |Valued    |TradPed   |SCRPed    |
|:---------------------|:--------:|:--------:|:--------:|
|ValObjectives         |**.50**   |          |          |
|IncrUnderstanding     |**.67**   |          |          |
|IncrInterest          |**.70**   |          |          |
|ClearResponsibilities |          |**.79**   |          |
|EffectiveAnswers      |          |**.76**   |          |
|Feedback              |          |**.66**   |          |
|ClearOrganization     |          |**.74**   |          |
|ClearPresentation     |          |**.78**   |          |
|MultPerspectives      |          |          |**.68**   |
|DEIintegration        |          |          |**.67**   |
|EquitableEval         |          |          |**.59**   |
|Feedback              |          |          |**.58**   |




### Produce and interpret correlations between the individual items of a given subscale and the subscale scores of all other subscales

To do this we need to have subscale scores. Conveniently, I can use the variable vectors created in an earlier step. I will score each of the scales if 75% of the items are non-missing.


```r
items$Valued <- sjstats::mean_n(items[,Valued_vars], .75)
items$TradPed <- sjstats::mean_n(items[,TradPed_vars], .75)
items$SCRPed <- sjstats::mean_n(items[,SCRPed_vars], .75)
items$Total <- sjstats::mean_n(items, .75)
```

For each subscale, we can produce an apaTables::apa.cor.table for the items-and-OtherScales.  Since there are 3 subscales, this is going to get spicy.

#### Valued-by-the-Student Items

First with the traditional pedagogy total scale score.


```r
apaTables::apa.cor.table(items[c('ValObjectives', 'IncrUnderstanding', 'IncrInterest', 'TradPed')])
```

```


Means, standard deviations, and correlations with confidence intervals
 

  Variable             M    SD   1          2          3         
  1. ValObjectives     4.52 0.61                                 
                                                                 
  2. IncrUnderstanding 4.28 0.82 .44**                           
                                 [.34, .52]                      
                                                                 
  3. IncrInterest      3.94 0.99 .48**      .68**                
                                 [.39, .56] [.62, .74]           
                                                                 
  4. TradPed           4.25 0.76 .50**      .62**      .61**     
                                 [.41, .58] [.55, .68] [.54, .68]
                                                                 

Note. M and SD are used to represent mean and standard deviation, respectively.
Values in square brackets indicate the 95% confidence interval.
The confidence interval is a plausible range of population correlations 
that could have caused the sample correlation (Cumming, 2014).
 * indicates p < .05. ** indicates p < .01.
 
```
After each analysis, I can update my table with the data representing the correlations with the individual items of one scale with the total scale score included in the correlation matrix. Our hope is that the corrected item-total correlations that we collected above will be stronger than the individual items' correlations with the other scales' total scores.

|Item-Total Correlations of Items with their Own and Other Subscales
|:------------------------------------------------------|

|Variables             |Valued    |TradPed   |SCRPed    |
|:---------------------|:--------:|:--------:|:--------:|
|ValObjectives         |**.50**   | .50      |          |
|IncrUnderstanding     |**.67**   | .62      |          |
|IncrInterest          |**.70**   | .61      |          |
|ClearResponsibilities |          |**.79**   |          |
|EffectiveAnswers      |          |**.76**   |          |
|Feedback              |          |**.66**   |          |
|ClearOrganization     |          |**.74**   |          |
|ClearPresentation     |          |**.78**   |          |
|MultPerspectives      |          |          |**.68**   |
|DEIintegration        |          |          |**.67**   |
|EquitableEval         |          |          |**.59**   |
|Feedback              |          |          |**.58**   |



Next, the Valued-by-the-Student Items with socially responsive pedagogy total scale score.


```r
apaTables::apa.cor.table(items[c('ValObjectives', 'IncrUnderstanding', 'IncrInterest', 'SCRPed')])
```

```


Means, standard deviations, and correlations with confidence intervals
 

  Variable             M    SD   1          2          3         
  1. ValObjectives     4.52 0.61                                 
                                                                 
  2. IncrUnderstanding 4.28 0.82 .44**                           
                                 [.34, .52]                      
                                                                 
  3. IncrInterest      3.94 0.99 .48**      .68**                
                                 [.39, .56] [.62, .74]           
                                                                 
  4. SCRPed            4.52 0.58 .41**      .44**      .54**     
                                 [.32, .50] [.35, .53] [.45, .61]
                                                                 

Note. M and SD are used to represent mean and standard deviation, respectively.
Values in square brackets indicate the 95% confidence interval.
The confidence interval is a plausible range of population correlations 
that could have caused the sample correlation (Cumming, 2014).
 * indicates p < .05. ** indicates p < .01.
 
```
|Item-Total Correlations of Items with their Own and Other Subscales
|:------------------------------------------------------|

|Variables             |Valued    |TradPed   |SCRPed    |
|:---------------------|:--------:|:--------:|:--------:|
|ValObjectives         |**.50**   | .50      |.41       |
|IncrUnderstanding     |**.67**   | .62      |.44       |
|IncrInterest          |**.70**   | .61      |.54       |
|ClearResponsibilities |          |**.79**   |          |
|EffectiveAnswers      |          |**.76**   |          |
|Feedback              |          |**.66**   |          |
|ClearOrganization     |          |**.74**   |          |
|ClearPresentation     |          |**.78**   |          |
|MultPerspectives      |          |          |**.68**   |
|DEIintegration        |          |          |**.67**   |
|EquitableEval         |          |          |**.59**   |
|Feedback              |          |          |**.58**   |


### Traditional Pedagogy Items

First, the traditional pedagogy items with the valued-by-the-student total scale score.


```r
apaTables::apa.cor.table(items[c('ClearResponsibilities', 'EffectiveAnswers', 'Feedback', 'ClearOrganization', 'ClearPresentation', 'Valued')])
```

```


Means, standard deviations, and correlations with confidence intervals
 

  Variable                 M    SD   1          2          3         
  1. ClearResponsibilities 4.44 0.82                                 
                                                                     
  2. EffectiveAnswers      4.36 0.83 .69**                           
                                     [.63, .74]                      
                                                                     
  3. Feedback              4.24 0.88 .63**      .58**                
                                     [.56, .70] [.50, .65]           
                                                                     
  4. ClearOrganization     4.01 1.08 .67**      .60**      .55**     
                                     [.61, .73] [.52, .67] [.46, .62]
                                                                     
  5. ClearPresentation     4.24 0.92 .69**      .72**      .55**     
                                     [.62, .74] [.66, .77] [.47, .62]
                                                                     
  6. Valued                4.25 0.68 .52**      .59**      .49**     
                                     [.43, .60] [.51, .66] [.40, .57]
                                                                     
  4          5         
                       
                       
                       
                       
                       
                       
                       
                       
                       
                       
                       
  .70**                
  [.63, .75]           
                       
  .63**      .69**     
  [.55, .69] [.63, .75]
                       

Note. M and SD are used to represent mean and standard deviation, respectively.
Values in square brackets indicate the 95% confidence interval.
The confidence interval is a plausible range of population correlations 
that could have caused the sample correlation (Cumming, 2014).
 * indicates p < .05. ** indicates p < .01.
 
```


|Item-Total Correlations of Items with their Own and Other Subscales
|:------------------------------------------------------|

|Variables             |Valued    |TradPed   |SCRPed    |
|:---------------------|:--------:|:--------:|:--------:|
|ValObjectives         |**.50**   | .50      |.41       |
|IncrUnderstanding     |**.67**   | .62      |.44       |
|IncrInterest          |**.70**   | .61      |.54       |
|ClearResponsibilities |.52       |**.79**   |          |
|EffectiveAnswers      |.59       |**.76**   |          |
|Feedback              |.49       |**.66**   |          |
|ClearOrganization     |.63       |**.74**   |          |
|ClearPresentation     |.69       |**.78**   |          |
|MultPerspectives      |          |          |**.68**   |
|DEIintegration        |          |          |**.67**   |
|EquitableEval         |          |          |**.59**   |
|Feedback              |          |          |**.58**   |


Next, the traditional pedagogy items with the socially responsive pedagogy total scale score.


```r
apaTables::apa.cor.table(items[c('ClearResponsibilities', 'EffectiveAnswers', 'Feedback', 'ClearOrganization', 'ClearPresentation', 'SCRPed')])
```

```


Means, standard deviations, and correlations with confidence intervals
 

  Variable                 M    SD   1          2          3         
  1. ClearResponsibilities 4.44 0.82                                 
                                                                     
  2. EffectiveAnswers      4.36 0.83 .69**                           
                                     [.63, .74]                      
                                                                     
  3. Feedback              4.24 0.88 .63**      .58**                
                                     [.56, .70] [.50, .65]           
                                                                     
  4. ClearOrganization     4.01 1.08 .67**      .60**      .55**     
                                     [.61, .73] [.52, .67] [.46, .62]
                                                                     
  5. ClearPresentation     4.24 0.92 .69**      .72**      .55**     
                                     [.62, .74] [.66, .77] [.47, .62]
                                                                     
  6. SCRPed                4.52 0.58 .64**      .60**      .62**     
                                     [.56, .70] [.52, .67] [.55, .69]
                                                                     
  4          5         
                       
                       
                       
                       
                       
                       
                       
                       
                       
                       
                       
  .70**                
  [.63, .75]           
                       
  .51**      .62**     
  [.43, .59] [.54, .68]
                       

Note. M and SD are used to represent mean and standard deviation, respectively.
Values in square brackets indicate the 95% confidence interval.
The confidence interval is a plausible range of population correlations 
that could have caused the sample correlation (Cumming, 2014).
 * indicates p < .05. ** indicates p < .01.
 
```


|Item-Total Correlations of Items with their Own and Other Subscales
|:------------------------------------------------------|

|Variables             |Valued    |TradPed   |SCRPed    |
|:---------------------|:--------:|:--------:|:--------:|
|ValObjectives         |**.50**   | .50      |.41       |
|IncrUnderstanding     |**.67**   | .62      |.44       |
|IncrInterest          |**.70**   | .61      |.54       |
|ClearResponsibilities |.52       |**.79**   |.64       |
|EffectiveAnswers      |.59       |**.76**   |.60       |
|Feedback              |.49       |**.66**   |.62       |
|ClearOrganization     |.63       |**.74**   |.51       |
|ClearPresentation     |.69       |**.78**   |.62       |
|MultPerspectives      |          |          |**.68**   |
|DEIintegration        |          |          |**.67**   |
|EquitableEval         |          |          |**.59**   |
|Feedback              |          |          |**.58**   |

#### Socially Responsive Pedagogy Items

First, the socially responsive pedagogy tems with the valued-by-the-student total scale score.


```r
apaTables::apa.cor.table(items[c('MultPerspectives', 'InclusvClassrm', 'DEIintegration','EquitableEval', 'Valued')])
```

```


Means, standard deviations, and correlations with confidence intervals
 

  Variable            M    SD   1          2          3          4         
  1. MultPerspectives 4.39 0.84                                            
                                                                           
  2. InclusvClassrm   4.61 0.68 .57**                                      
                                [.49, .64]                                 
                                                                           
  3. DEIintegration   4.53 0.74 .50**      .62**                           
                                [.41, .59] [.54, .69]                      
                                                                           
  4. EquitableEval    4.57 0.63 .59**      .47**      .37**                
                                [.51, .66] [.37, .55] [.27, .47]           
                                                                           
  5. Valued           4.25 0.68 .54**      .48**      .29**      .46**     
                                [.45, .61] [.38, .56] [.18, .40] [.37, .54]
                                                                           

Note. M and SD are used to represent mean and standard deviation, respectively.
Values in square brackets indicate the 95% confidence interval.
The confidence interval is a plausible range of population correlations 
that could have caused the sample correlation (Cumming, 2014).
 * indicates p < .05. ** indicates p < .01.
 
```

|Item-Total Correlations of Items with their Own and Other Subscales
|:------------------------------------------------------|

|Variables             |Valued    |TradPed   |SCRPed    |
|:---------------------|:--------:|:--------:|:--------:|
|ValObjectives         |**.50**   | .50      |.41       |
|IncrUnderstanding     |**.67**   | .62      |.44       |
|IncrInterest          |**.70**   | .61      |.54       |
|ClearResponsibilities |.52       |**.79**   |.64       |
|EffectiveAnswers      |.59       |**.76**   |.60       |
|Feedback              |.49       |**.66**   |.62       |
|ClearOrganization     |.63       |**.74**   |.51       |
|ClearPresentation     |.69       |**.78**   |.62       |
|MultPerspectives      |.54       |          |**.68**   |
|DEIintegration        |.48       |          |**.67**   |
|EquitableEval         |.29       |          |**.59**   |
|Feedback              |.46       |          |**.58**   |


Next, the socially responsive pedagogy items with the traditional pedagogy total scale score.


```r
apaTables::apa.cor.table(items[c('MultPerspectives', 'InclusvClassrm', 'DEIintegration','EquitableEval', 'TradPed')])
```

```


Means, standard deviations, and correlations with confidence intervals
 

  Variable            M    SD   1          2          3          4         
  1. MultPerspectives 4.39 0.84                                            
                                                                           
  2. InclusvClassrm   4.61 0.68 .57**                                      
                                [.49, .64]                                 
                                                                           
  3. DEIintegration   4.53 0.74 .50**      .62**                           
                                [.41, .59] [.54, .69]                      
                                                                           
  4. EquitableEval    4.57 0.63 .59**      .47**      .37**                
                                [.51, .66] [.37, .55] [.27, .47]           
                                                                           
  5. TradPed          4.25 0.76 .71**      .54**      .34**      .65**     
                                [.64, .76] [.46, .62] [.23, .44] [.58, .71]
                                                                           

Note. M and SD are used to represent mean and standard deviation, respectively.
Values in square brackets indicate the 95% confidence interval.
The confidence interval is a plausible range of population correlations 
that could have caused the sample correlation (Cumming, 2014).
 * indicates p < .05. ** indicates p < .01.
 
```


|Item-Total Correlations of Items with their Own and Other Subscales
|:------------------------------------------------------|

|Variables             |Valued    |TradPed   |SCRPed    |
|:---------------------|:--------:|:--------:|:--------:|
|ValObjectives         |**.50**   | .50      |.41       |
|IncrUnderstanding     |**.67**   | .62      |.44       |
|IncrInterest          |**.70**   | .61      |.54       |
|ClearResponsibilities |.52       |**.79**   |.64       |
|EffectiveAnswers      |.59       |**.76**   |.60       |
|Feedback              |.49       |**.66**   |.62       |
|ClearOrganization     |.63       |**.74**   |.51       |
|ClearPresentation     |.69       |**.78**   |.62       |
|MultPerspectives      |.54       |.71       |**.68**   |
|InclusvClassrm        |.48       |.54       |**.67**   |
|DEIintegration        |.29       |.34       |**.59**   |
|EquitableEval         |.46       |.65       |**.58**   |




### APA style results section with table

* Brief description of each step
* Brief instructions for interpreting results
* Presentation of results

>>Item analyses were conducted on the 12 course evaluation items that were selected to represent the Valued-by-Me, Traditional Pedagogy, and Socially & Culturally Responsive Pedgagy subscales. To assess the within-scale convergent and discrimninant validity of these three subscales, each item was correlated with its own scale (with the item removed) and with the other course evaluation scales (see Table 1). For the Valued and TradPed dimensions, items were more highly correlated with their own scale than with the other scale. For the SCRPed subscale, two items (MultPerspectives, EquitableEval) had higher correlations with TradPed than with their hypothesized subscale (SCRPed). Coefficient alphas were .77, .90, .81, and .92 for the Valued, TradPed, SCRPed, and total-scale scores, respectively. We conclude that more work is needed to create distinct and stable subscales. 


### Explanation to grader








