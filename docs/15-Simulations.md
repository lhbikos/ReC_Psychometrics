
# Additional Simulations {#sims}

[Screencast Link](https://www.youtube.com/playlist?list=PLtz5cFLQl4KOOKKTNWJqTSUjx2Nm0D2ON)



In each of the suggestions for practice (i.e., "homework"), I suggest that an option for a middle-level degree of difficulty is to use data from another set of simulated data. One option is to use simulations from other lessons. Especially in the early chapters, it is difficult to know what data from later chapters might be appropriate for such analyses. Because of this challenge, I am providing several simulations that are not used in any of the lessons that could be used as practice for *all* of the lessons that involve psychometric evaluation. In this way, you would follow the construction of a scale through the standard process. 

There are a few caveats to this process:

* In each of the simulations, I have added the code, "eval = FALSE" in the top of the chunk. This prevents the chunk from executing when the OER is *building*. If you copy the script you should have no problems (but if you try to knit an .rmd file and wonder why no data is being produced, this is why).
* Each of the psychometric evaluations included a number of additional measures used to assess convergent, discriminant, concurrent, predictive, and incremental validity. While I would have liked to have included them all, 
  - I could not always locate source articles, and 
  - Adding too many scales caused my simulation code to fail. 
  - Thus, each simulation includes at least three additional measures that can be used for evaluating validity as it relates to measures within the nomological net (e.g., convergent, discriminant, concurrent, predictive, incremental).
* There are two simulations with each scale.
  - The first simulation provides the focal scale and the additional instruments.
  - The second simulation creates "A" and "B" data for the focal scale. When you are practicing test-retest reliability, you can *pretend* that A and B are from the same respondents. Later, when you are practicing invariance testing you can *pretend* that the data are from two different groups.
* At least one of these scales as five subscales. In certain analyses (e.g., item analysis) this may become unwieldy. In such cases you may wish to select three of those subscales and run the analyses with just those. After all, "it's just practice." I do recommend that you complete the majority of practice assignments with a minimum of three subscales.
* Each of the simulations includes a random seed. If you and homework partners would like to work on the same simulation, you could gently increase your challenge by setting different random seeds and comparing the subtle differences in the solutions.
* I  recommend that you retrieve the original psychometric article so that you can compare your analytic choices and results with those completed in the article. At least two of the articles are available as preprints or in open-source journals.

## iBelong Scale 

The iBelong Scale [@lee_ibelong_2024] is a measure of racial-ethnic-cultural (REC) belonging for BIPOC people. The scale includes 25 items with responses rated on a 6-point Likert scale ranging from 1 (*strongly disagree*) to 6 (*strongly agree*). At the start of the survey, participants are asked to self-identify their REC identity (i.e., "In terms of my racial-ethnic-cultural [REC] identity I consider myself to be:____"). Higher scores indicate a stronger sense of REC belonging. Lee and Neville [-@lee_ibelong_2024] reported that a five-factor solution resulted in the best fit.

Beneath each of the five factors are a list of the items; variable names follow in parentheses.

* Authenticity:  
  - In general, I do not have to change my behaviors when I am with REC group members (Auth1)
  - I am free to be myself with members of my REC group (Auth2)
  - In general, I do not have to hide parts of who I am with members of my REC group (Auth3)
  - Members of my REC group see me for who I am (Auth4)
  - I feel accepted by my REC group for who I am (Auth5)
* Connection:  
  - I have similar experiences to others in my REC group (Conn1)
  - Others in my REC group see the world in a similar way as me (Conn2)
  - My success is connected to the success of members of my REC group (Conn3)
  - I have many things in common with people from my REC group (Conn4)
  - I feel connected to my REC group because of our shared experiences (Conn5)
* Home
  - I feel close to other members of my REC group (Home1)
  - I have shared interests with others in my REC group (Home2)
  - I have shared values with others in my REC group (Home3)
  - In general, I am at ease when I am with people from my REC group (Home4)
  - In general, I feel “at home” when I am with members of my REC group (Home5)
* REC Thriving
  - I am happy that I am a member of my REC group (Thriv1)
  - I am proud to be a member of my REC group (Thriv2)
  - I like learning about my REC group’s history (Thriv3)
  - I value my REC group (Thriv4)
  - I consider it an honor to be a member of my REC group (Thriv5) 
*Self-Definition
  - I define what belonging to my REC group means to me (Self1)
  - I am a member of my REC group on my own terms (Self2)
  - I decide what my REC group membership is (Self3)
  - I do not have to prove that I belong to my REC group to others in my REC group (Self4)
  - Others do not define my belonging to my REC group (Self5)


A [preprint](https://www.researchgate.net/publication/377700068_The_iBelong_Scale_Construction_and_validation_of_a_measure_of_racial-ethnic-cultural_belonging) of the article is available at ResearchGate. Below is the script for simulating item-level data from the factor loadings, means, and sample size presented in the published article. 

Six additional scales were reported in the Lee and Neville [-@lee_ibelong_2024] article. Optimizing the ability for the simulation to converge and also to provide an array of scales within the nomological net, I chose the three scales below. Unfortunately, I could not locate factor loadings for all of them; in these cases, I uniformly assigned the factor loading of 0.8. The scales, their original citation, and information about how I simulated data for each are listed below.

* **General Belongingness Scale** [GBS; @malone_general_2012] is a 12-item item scale with Likert scaling ranging from 1 (*strongly disagree*) to 7 (*strongly agree*). There are two six-item subscales:  Acceptance/Inclusion ("When I am with other people, I feel included") and Rejection/Exclusion ("I feel like an outsider"). The items on the Rejection/Exclusion subscale must be rescored such that higher scores represent a greater sense of belonging in general. In the iBELONG study [@lee_ibelong_2024], only a total GBS scale was used. My simulation used factor loadings from Malone et al. [-@malone_general_2012] but treated them as a single scale. This means that there is need to reverse-score the Rejection/Exclusion items in this simulated data.
* **The Collective Self-Esteem Scale--Race Specific Version** [CSESR; @crocker_collective_1994] is a 16-item scale with Likert scaling ranging from 1 (*strongly disagree*) to 7 (*strongly agree*). Higher scores represent a stronger sense of membership with one's own racial/ethnic group. There are four, four-item subscales: Membership CSE, Public CSE, Private CSE, and Importance to Identity, however the IBelong study [@lee_ibelong_2024] used a total scale score. An example item is, "The racial-ethnic group I belong to is an important reflection of who I am." Because I was not able to locate factor loadings from a psychometric evaluation, I simulated the data by specifying a 0.8 as a standardized factor loading for each of the items on the general factor.
* **The Multigroup Ethnic Identity Measure -- Revised** [MEIMR; @brown_multigroup_2014] is a 7-item scale. The first item is an open-ended question for identification of respondent ethnic group. The remaining six items are assessed with Likert scaling ranging from 1 (*strongly disagree*) to 5 (*strongly agree*). There are two, three-item subscales which assess exploration (e.g., "I have spent time trying to find out more about my ethnic group, such as its history, tradition, and customs") and commitment ("I have a strong sense of belonging to my own ethnic group.") Higher scores indicate more positive ethnic identity. In the iBELONG study [@lee_ibelong_2024], only a total MEIMR scale was used. My simulation used factor loadings from Brown et al. [-@brown_multigroup_2014] but treated them as a single scale. 

Because data is collected at the item level (and I want this resource to be as practical as possible, I have simulated the data for each of the scales at the item level. Simulating the data involved using factor loadings, means, and correlations between the scales. Because the simulation will produce "out-of-bounds" values, the code below re-scales the scores into the range of the Likert-type scaling and rounds them to whole values.


```r
#Entering the intercorrelations, means, and standard deviations from the journal article

iBelong_generating_model <- '
        #measurement model
        Authenticity  =~ .66*Auth1 + .64*Auth2 + .63*Auth3 + .58*Auth4 + .55*Auth5 
        Connection =~ .72*Conn1 + .60*Conn2 + .59*Conn3 + .58*Conn4 + .58*Conn5
        Home =~ .64*Home1 + .63*Home2 + .57*Home3 + .57*Home4 + .53*Home5
        RECthriving =~ .68*Thriv1 + .66*Thriv2 + .59*Thriv3 + .54*Thriv4 + .49*Thriv5
        SelfDefinition =~ .82*Self1 + .65*Self2 + .65*Self3 + .54*Self4 + .49*Self5
        GBS =~ .70*GBS1 + .67*GBS2 + .65*GBS5 + .67*GBS8 + .70*GBS10 + .78*GBS11 + .78*GBS3 + .66*GBS4 + .77*GBS6 + .82*GBS7 + .79*GBS9 + .66*GBS12
        CSESR =~ .8*CSESR1 + .8*CSESR2 + .8*CSESR3 + .8*CSESR4 + .8*CSESR5 + .8*CSESR6 + .8*CSESR7 + .8*CSESR8 + .8*CSESR9 + .8*CSESR10 + .8*CSESR11 + .8*CSESR12 + .8*CSESR13 + .8*CSESR14 + .8*CSESR15 + .8*CSESR16 
        MEIMR =~ .60*MEIMR1 + .93*MEIMR4 + .81*MEIMR5 + .86*MEIMR2 + .84*MEIMR3 + .89*MEIMR6
        
        #Means
         Authenticity ~ 4.30*1
         Connection ~ 4.16*1
         Home ~ 4.51*1
         RECthriving ~ 4.81*1
         SelfDefinition ~ 4.53*1
         GBS ~ 4.84*1
         CSESR ~ 5.15*1
         MEIMR ~ 3.81*1

         #Correlations
         Authenticity ~~ .73*Connection
         Authenticity ~~ .78*Home
         Authenticity ~~ .64*RECthriving
         Authenticity ~~ .52*SelfDefinition
         Authenticity ~~ .58*GBS
         Authenticity ~~ .58*CSESR
         Authenticity ~~ .48*MEIMR
         
         Connection ~~ .81*Home
         Connection ~~ .70*RECthriving
         Connection ~~ .43*SelfDefinition
         Connection ~~ .36*GBS
         Connection ~~ .63*CSESR
         Connection ~~ .62*MEIMR
         
         Home ~~ .74*RECthriving
         Home ~~ .48*SelfDefinition
         Home ~~ .51*GBS
         Home ~~ .65*CSESR
         Home ~~ .63*MEIMR
         
         RECthriving ~~ .46*SelfDefinition
         RECthriving ~~ .42*GBS
         RECthriving ~~ .70*CSESR
         RECthriving ~~ .70*MEIMR
         
         SelfDefinition ~~ .29*GBS
         SelfDefinition ~~ .38*CSESR
         SelfDefinition ~~ .35*MEIMR
         
         '

set.seed(240326)
iBel <- lavaan::simulateData(model = iBelong_generating_model,
                              model.type = "sem",
                              meanstructure = T,
                              sample.nobs=500,
                              standardized=FALSE)

#used to retrieve column indices used in the rescaling script below
col_index <- as.data.frame(colnames(iBel))

#The code below loops through each column of the dataframe and assigns the scaling accordingly
#Rows 1 thru 25 are the iBelong scale
#Rows 26 thru 37 are the General Belonging Scale
#Rows 38 thru 53 are the Collective Self Esteem Scale Race Specific Version
#Rows 54 thru 59 are the Multigroup Etnic Identity measure Revised


for(i in 1:ncol(iBel)){  
  if(i >= 1 & i <= 25){   
    iBel[,i] <- scales::rescale(iBel[,i], c(1, 6))
  }
    if(i >= 26 & i <= 37){   
    iBel[,i] <- scales::rescale(iBel[,i], c(1, 7))
    }
      if(i >= 38 & i <= 53){  
    iBel[,i] <- scales::rescale(iBel[,i], c(1, 7))
      }
        if(i >= 54 & i <= 59){  
    iBel[,i] <- scales::rescale(iBel[,i], c(1, 5))
        }
}

#rounding to integers so that the data resembles that which was collected
library(tidyverse)
iBel <- iBel %>% round(0) 

#quick check of my work
#psych::describe(iBel) 
```

The optional script below will let you save the simulated data to your computing environment as either an .rds object (preserves any formatting you might do)  or a.csv file (think "Excel lite").


```r
# to save the df as an .rds (think 'R object') file on your computer;
# it should save in the same file as the .rmd file you are working
# with saveRDS(iBel, 'iBel.rds') bring back the simulated dat from an
# .rds file iBel <- readRDS('iBel.rds')
```


```r
# write the simulated data as a .csv write.table(iBel,
# file='iBel.csv', sep=',', col.names=TRUE, row.names=FALSE) bring
# back the simulated dat from a .csv file iBel <-
# read.csv('iBel.csv', header = TRUE)
```

Lessons in this volume teach test-retest reliability and invariance testing. In both of these circumstances, data from two different administrations of the focal test are required. For test-retest, these would be completed by the same person; for invariance-testing, these would be completed by different people. Below I have simulated two sets of data for the iBelong Scale [@lee_ibelong_2024]. I have named them "A" and "B". For your homework purposes, you can determine if they will represent testing with the same individual (appropriate for test-retest reliability) or different groups (appropriate for invariance testing).


```r
iBelong_generating_modelAB <- '
        #measurement model
        AuthenticityA  =~ .66*Auth1a + .64*Auth2a + .63*Auth3a + .58*Auth4a + .55*Auth5a
        ConnectionA =~ .72*Conn1a + .60*Conn2a + .59*Conn3a + .58*Conn4a + .58*Conn5a
        HomeA =~ .64*Home1a + .63*Home2a + .57*Home3a + .57*Home4a + .53*Home5a
        RECthrivingA =~ .68*Thriv1a + .66*Thriv2a + .59*Thriv3a + .54*Thriv4a + .49*Thriv5a
        SelfDefinitionA =~ .82*Self1a + .65*Self2a + .65*Self3a + .54*Self4a + .49*Self5a
        AuthenticityB  =~ .63*Auth1b + .68*Auth2b + .69*Auth3b + .52*Auth4b + .54*Auth5b
        ConnectionB =~ .70*Conn1b + .63*Conn2b + .55*Conn3b + .54*Conn4b + .54*Conn5b
        HomeB =~ .60*Home1b + .64*Home2b + .51*Home3b + .52*Home4b + .59*Home5b
        RECthrivingB =~ .66*Thriv1b + .64*Thriv2b + .52*Thriv3b + .59*Thriv4b + .53*Thriv5b
        SelfDefinitionB =~ .75*Self1b + .69*Self2b + .68*Self3b + .57*Self4b + .53*Self5b

   
        #Means
         AuthenticityA ~ 4.30*1
         ConnectionA ~ 4.16*1
         HomeA ~ 4.51*1
         RECthrivingA ~ 4.81*1
         SelfDefinitionA ~ 4.53*1
        
         AuthenticityB ~ 4.28*1
         ConnectionB ~ 4.20*1
         HomeB ~ 4.44*1
         RECthrivingB ~ 4.9*1
         SelfDefinitionB ~ 4.49*1
         
         #Correlations
         AuthenticityA ~~ .81*AuthenticityB
         ConnectionA ~~ .85*ConnectionB
         HomeA ~~ .77*HomeB
         RECthrivingA ~~ .85*RECthrivingB
         SelfDefinitionA ~~ .84*SelfDefinitionB
        
         '

set.seed(240326)
iBelAB <- lavaan::simulateData(model = iBelong_generating_modelAB,
                              model.type = "sem",
                              meanstructure = T,
                              sample.nobs=500,
                              standardized=FALSE)

#used to retrieve column indices used in the rescaling script below
col_index <- as.data.frame(colnames(iBelAB))

#The code below loops through each column of the dataframe and assigns the scaling accordingly
#All rows are the iBel scales, administrations A and B


for(i in 1:ncol(iBelAB)){  
  if(i >= 1 & i <= 50){   
    iBelAB[,i] <- scales::rescale(iBelAB[,i], c(1, 6))
  }
}

#rounding to integers so that the data resembles that which was collected
library(tidyverse)
iBelAB <- iBelAB %>% round(0) 

#quick check of my work
psych::describe(iBelAB) 
```
If you want to use the data for invariance testing, the data will need to be in *long* form. Here's code to get it there. 


```r
# First creating a tiny df with just the GroupA observations Add an
# ID variable to each row
iBelA <- dplyr::select(iBelAB, Auth1a, Auth2a, Auth3a, Auth4a, Auth5a,
    Conn1a, Conn2a, Conn3a, Conn4a, Conn5a, Home1a, Home2a, Home3a, Home4a,
    Home5a, Thriv1a, Thriv2a, Thriv3a, Thriv4a, Thriv5a)
# adding a variable to indicate these are from Group A
iBelA$Group <- "GroupA"
# renaming so that when I bind the A and B dfs they have the same
# variable names
iBelA <- dplyr::rename(iBelA, Auth1 = "Auth1a", Auth2 = "Auth2a", Auth3 = "Auth3a",
    Auth4 = "Auth4a", Auth5 = "Auth5a", Conn1 = "Conn1a", Conn2 = "Conn2a",
    Conn3 = "Conn3a", Conn4 = "Conn4a", Conn5 = "Conn5a", Home1 = "Home1a",
    Home2 = "Home2a", Home3 = "Home3a", Home4 = "Home4a", Home5 = "Home5a",
    Thriv1 = "Thriv1a", Thriv2 = "Thriv2a", Thriv3 = "Thriv3a", Thriv4 = "Thriv4a",
    Thriv5 = "Thriv5a")

# Second creating a tiny df with just the GroupB observations
iBelB <- dplyr::select(iBelAB, Auth1b, Auth2b, Auth3b, Auth4b, Auth5b,
    Conn1b, Conn2b, Conn3b, Conn4b, Conn5b, Home1b, Home2b, Home3b, Home4b,
    Home5b, Thriv1b, Thriv2b, Thriv3b, Thriv4b, Thriv5b)
# adding a variable to indicate these are from Group B
iBelB$Group <- "GroupB"
# renaming so that when I bind the A and B dfs they have the same
# variable names
iBelB <- dplyr::rename(iBelB, Auth1 = "Auth1b", Auth2 = "Auth2b", Auth3 = "Auth3b",
    Auth4 = "Auth4b", Auth5 = "Auth5b", Conn1 = "Conn1b", Conn2 = "Conn2b",
    Conn3 = "Conn3b", Conn4 = "Conn4b", Conn5 = "Conn5b", Home1 = "Home1b",
    Home2 = "Home2b", Home3 = "Home3b", Home4 = "Home4b", Home5 = "Home5b",
    Thriv1 = "Thriv1b", Thriv2 = "Thriv2b", Thriv3 = "Thriv3b", Thriv4 = "Thriv4b",
    Thriv5 = "Thriv5b")

# Binding the A and B sets of data use this df for the invariance
# homework
iBelLONG <- rbind(iBelA, iBelB)
```



## Identity Threat 

The Identity Threat Scale [@george_when_2023]is a measure of threat to identity value, meanings, and enactment. The measure is designed to adapt to different identities. The scale includes 19 items with responses rated on a 6-point Likert scale ranging from 1 (*strongly disagree*) to 5 (*strongly agree*). Items are written such that researchers can provide the focal identity (e.g., "a teacher," "LGBTQ"). Across all three scales, higher scores reflect higher threat. It appears that the authors landed on a single-order, correlated factors, structure. 

Beneath each of the three factors are a list of the items. Variable names follow in parentheses.

* Identity Value:  
  - I feel that there is a negative value attached to my identity as [LGBTQ]. (Val1)
  - Being [LGBTQ] is worth less in the eyes of others than before. (Val2)
  - I feel that others attach a negative value to my identity as [LGBTQ]. (Val3)
  - I feel that my identity as [LGBTQ] is devalued by others. (Val4)
  - I feel that others see little value in my identity as [LGBTQ].(Val5)
* Identity Meaning:  
  - I am no longer sure what it means to be [LGBTQ].(Mng1)
  - I am questioning what it means to be [LGBTQ]. (Mng2)
  - I find myself questioning what it means to be [LGBTQ]. (Mng3)
  - The core of what it means to be [LGBTQ] is changing in a way I do not like. (Mng4)
  - What it means to be [LGBTQ] is changing in a way I do not like. (Mng5)
  - What it means to be [LGBTQ] is being called into question. (Mng6)
  - Being [LGBTQ] used to mean something different. (Mng7)
  -I feel that being [LGBTQ] does not mean the same thing anymore. (Mng8)
* Identity Enactment
  - I am limited in my ability to express my identity as [LGBTQ]. (Enact1)
  - I may no longer be able to engage in activities that express my identity as [LGBTQ]. (Enact2)
  - I may no longer be able to show that I am [LGBTQ]. (Enact3)
  - I worry about no longer being able to express my identity as [LGBTQ]. (Enacte4)
  - I worry that I cannot behave in the way [an LGBTQ person] behaves. (Enact5)
  - I worry that I cannot show people that I am [LGBTQ]. (Enact6)

Although I have simulated data, the authors posted their data and codebooks from the different phases at the [OSF repository](https://osf.io/b5hrt/?view_only=c1f17b92103c47c8abc9fb795056cbb9). Additional materials are available as a [supplement](https://supp.apa.org/psycarticles/supplemental/apl0001114/APL-2022-3613_Supplemental_Materials.pdf) to the article.

There were a number of scales utilized in this study. Because including them all caused problems of convergence, beyond the subscales in the focal measure, I have simulated data for only a few more. This will provide practice in evaluating convergent, discriminant, and incremental validity.

* **Self-esteem** was assessed with [Rosenberg's 10-item scale](https://www.apa.org/obesity-guideline/rosenberg-self-esteem.pdf). Responses are measured on a 4-point Likert scale ranging from 1 (*strongly agree*) to 4 (*strongly disagree*). Some items are reverse-coded. However, using the data from this simulation presumes that reverse-scoring has already been completed. Higher scores indicate higher self-esteem. An example item is "On the whole, I am satisfied with myself." Factor loadings were obtained from Mullen et al. [-@mullen_evaluation_2013].
* **Identity suppression** was assessed with 4 items from Madera et al.'s [-@madera_bringing_2012] 10 item scale. It is a bit unclear, but it appears that items were rated on a 1 (*strongly disagree*) to 7 (*strongly agree*) scale with higher scores reflecting higher identity suppression. A sample item is, "I refrain from talking about my identity as LGBTQ at work."
* **Workplace microaggressions** was captured with 11 items from Resnick and Galupo's [@resnick_assessing_2019] scale. Responses are measured on a Likert type scale ranging from 1 (*never*) to 5 (*a great deal*). Higher scores indicate higher frequency of microaggressions. An example item is "Having my behaviors mimicked in a joking way due to my LGBTQ identity." It is unclear if they used one or more scales. I simulated the data from Resnick and Galupo, selecting 3 and 4 items from three subscales.
* **Green behaviors** were captured with three items from Norton et al.'s [@norton_bridging_2017] scale. Responses are measured on a Likert scale ranging from 1 (*strongly disagree*) to 5 (*strongly agree*). The response stem was, "Tomorrow, I intend to..." and items included, "...act in environmentally friendly ways," "...carry out environmentally friendly behaviors at work," and "...perform pro-environmental behaviors while at work. In the absence of factor loadings, I made them up.

Because data is collected at the item level (and I want this resource to be as practical as possible, I have simulated the data for each of the scales at the item level. I guided the simulation using factor loadings from the exploratory factor analysis results and means and correlations from the Stage 5 analysis where 516 individuals who identified as LGBTQ completed the survey. Because the simulation will produce "out-of-bounds" values, the code below rescales the scores into the range of the Likert-type scaling and rounds them to whole values.


```r
#Entering the intercorrelations, means, and standard deviations from the journal article

IdentityThreat_generating_model <- '
        #measurement model
        Value  =~ .83*Val1 + .78*Val2 + .88*Val3 + .80*Val4 + .73*Val5
        Meaning =~ .66*Mng1 + .81*Mng2 + .85*Mng3 + .78*Mng4 + .74*Mng5 + .64*Mng6 + .65*Mng7 + .73*Mng8
        Enactment =~ .66*Enact1 + .64*Enact2 + .82*Enact3 + .70*Enact4 + .66*Enact5 + .94*Enact6
        SelfEsteem =~ .95*SE1 + .98*SE2 + .66*SE3 + .81*SE4 + .55*SE5 + .80*SE6 + .75*SE7 + .66*SE8 + .78*SE9 + .76*SE10
        IDsuppression =~ .78*IDs1 + .67*IDs2 + .82*IDs3 + .90*IDs4
        WkplcMicroAgg =~ .84*Micro1 + .87*Micro2 + .72*Micro3 + .78*Micro4 + .67*Micro5 + .81*Micro6 + .63*Micro7 + .50*Micro8 + .58*Micro9 + .83*Micro10 + .63*Micro11
        GreenBx =~ .77*G1 + .81*G2 + .83*G3
       
        #Means
         Value ~ 2.15*1
         Meaning ~ 2.10*1
         Enactment ~ 2.17*1
         SelfEsteem ~ 3.44*1
         IDsuppression ~ 3.13*1
         WkplcMicroAgg ~ 1.24*1
         GreenBx ~ 3.49*1
      
        #Correlations
         Value ~~ .58*Meaning
         Value ~~ .73*Enactment
         Value ~~ -.21*SelfEsteem
         Value ~~ .35*IDsuppression
         Value ~~ .41*WkplcMicroAgg
         Value ~~ -.09*GreenBx
         
         Meaning ~~ .60*Enactment
         Meaning ~~ .63*SelfEsteem
         Meaning ~~ .26*IDsuppression
         Meaning ~~ .24*WkplcMicroAgg
         Meaning ~~ -.08*GreenBx
         
         Enactment ~~ -.31*SelfEsteem
         Enactment ~~ .54*IDsuppression
         Enactment ~~ .24*WkplcMicroAgg
         Enactment ~~ -.06*GreenBx
         
         SelfEsteem ~~ -.24*IDsuppression
         SelfEsteem ~~ -.06*WkplcMicroAgg
         SelfEsteem ~~ .15*GreenBx
         
         IDsuppression ~~ .00*WkplcMicroAgg
         IDsuppression ~~ -.02*GreenBx

        '

set.seed(240330)
IdThreat <- lavaan::simulateData(model = IdentityThreat_generating_model,
                              model.type = "sem",
                              meanstructure = T,
                              sample.nobs=516,
                              standardized=FALSE)

#used to retrieve column indices used in the rescaling script below
col_index <- as.data.frame(colnames(IdThreat))

#The code below loops through each column of the dataframe and assigns the scaling accordingly
#Rows 1 thru 19 are the Identity Threat
#Rows 20 thru 29 are Self Esteem
#Rows 30 thru 33 are Identity Suppression
#Rows 34 thru 44 are Workplace Microaggessions
#Rows 45 thru 47 are Green Behaviors

for(i in 1:ncol(IdThreat)){  
  if(i >= 1 & i <= 19){   
   IdThreat[,i] <- scales::rescale(IdThreat[,i], c(1, 7))
  }
    if(i >= 20 & i <= 29){   
    IdThreat[,i] <- scales::rescale(IdThreat[,i], c(1, 4))
    }
    if(i >= 30 & i <= 33){   
    IdThreat[,i] <- scales::rescale(IdThreat[,i], c(1, 7))
      }
    if(i >= 34 & i <= 44){   
    IdThreat[,i] <- scales::rescale(IdThreat[,i], c(1, 5))
    }
    if(i >= 45 & i <= 47){   
    IdThreat[,i] <- scales::rescale(IdThreat[,i], c(1, 5))
    }
}

#rounding to integers so that the data resembles that which was collected
library(tidyverse)
IdThreat <- IdThreat %>% round(0) 

#quick check of my work
#psych::describe(IdThreat) 
```

The optional script below will let you save the simulated data to your computing environment as either an .rds object (preserves any formatting you might do)  or a.csv file (think "Excel lite").


```r
# to save the df as an .rds (think 'R object') file on your computer;
# it should save in the same file as the .rmd file you are working
# with saveRDS(IdThreat, 'IdThreat.rds') bring back the simulated dat
# from an .rds file IdThreat <- readRDS('IdThreat.rds')
```


```r
# write the simulated data as a .csv write.table(IdThreat,
# file='IdThreat.csv', sep=',', col.names=TRUE, row.names=FALSE)
# bring back the simulated dat from a .csv file IdThreat <-
# read.csv('IdThreat.csv', header = TRUE)
```

Lessons in this volume teach test-retest reliability and invariance testing. In both of these circumstances, data from two different administrations of the focal test are required. For test-retest, these would be completed by the same person; for invariance-testing, these would be completed by different people. Below I have simulated two sets of data for The Identity Threat Scale [@george_when_2023]. I have named them "A" and "B". For your homework purposes, you can determine if they will represent testing with the same individual (appropriate for test-retest reliability) or different groups (appropriate for invariance testing).


```r
idThreat_generating_modelAB <- '
        #measurement model
        ValueA  =~ .83*Val1a + .78*Val2a + .88*Val3a + .80*Val4a + .73*Val5a
        MeaningA =~ .66*Mng1a + .81*Mng2a + .85*Mng3a + .78*Mng4a + .74*Mng5a + .64*Mng6a + .65*Mng7a + .73*Mng8a
        EnactmentA =~ .66*Enact1a + .64*Enact2a + .82*Enact3a + .70*Enact4a + .66*Enact5a + .94*Enact6a
        ValueB  =~ .87*Val1b + .72*Val2b + .85*Val3b + .76*Val4b + .70*Val5b
        MeaningB =~ .69*Mng1b + .89*Mng2b + .82*Mng3b + .72*Mng4b + .78*Mng5b + .60*Mng6b + .69*Mng7b + .71*Mng8b
        EnactmentB =~ .61*Enact1b + .62*Enact2b + .75*Enact3b + .75*Enact4b + .69*Enact5b + .82*Enact6b

        #Means
         ValueA ~ 1.97*1
         MeaningA ~ 2.16*1
         EnactmentA ~ 2.14*1
         ValueB ~ 2.10*1
         MeaningB ~ 2.28*1
         EnactmentB ~ 2.24*1
         
         
         #Correlations
         ValueA ~~ .80*MeaningA
         ValueA ~~ .80*EnactmentA
         ValueA ~~ .63*ValueB
         ValueA ~~ .57*MeaningB
         ValueA ~~ .56*EnactmentB
         
         MeaningA ~~ .77*EnactmentA
         MeaningA ~~ .59*ValueB
         MeaningA ~~ .70*MeaningB
         MeaningA ~~ .58*EnactmentB
         
         EnactmentA ~~ .54*ValueB
         EnactmentA ~~ .79*MeaningB
         EnactmentA ~~ .66*EnactmentB
         
         ValueB ~~ .81*MeaningB
         ValueB ~~ .82*EnactmentB
         
         MeaningB ~~ .81*EnactmentB
        
         '

set.seed(240326)
idThreatAB <- lavaan::simulateData(model = idThreat_generating_modelAB,
                              model.type = "sem",
                              meanstructure = T,
                              sample.nobs=500,
                              standardized=FALSE)

#used to retrieve column indices used in the rescaling script below
col_index <- as.data.frame(colnames(idThreatAB))

#The code below loops through each column of the dataframe and assigns the scaling accordingly
#All rows are the iBel scales, administrations A and B


for(i in 1:ncol(idThreatAB)){  
  if(i >= 1 & i <= 38){   
    idThreatAB[,i] <- scales::rescale(idThreatAB[,i], c(1, 5))
  }
}

#rounding to integers so that the data resembles that which was collected
library(tidyverse)
idThreatAB <- idThreatAB %>% round(0) 

#quick check of my work
#psych::describe(iBelAB) 
```


If you want to use the data for invariance testing, the data will need to be in *long* form. Here's code to get it there. 


```r
# First creating a tiny df with just the GroupA observations Add an
# ID variable to each row
IdThreatA <- dplyr::select(idThreatAB, Val1a, Val2a, Val3a, Val4a, Val5a,
    Mng1a, Mng2a, Mng3a, Mng4a, Mng5a, Mng6a, Mng7a, Mng8a, Enact1a, Enact2a,
    Enact3a, Enact4a, Enact5a, Enact6a)
# adding a variable to indicate these are from Group A
IdThreatA$Group <- "GroupA"
# renaming so that when I bind the A and B dfs they have the same
# variable names
IdThreatA <- dplyr::rename(IdThreatA, Val1 = "Val1a", Val2 = "Val2a", Val3 = "Val3a",
    Val4 = "Val4a", Val5 = "Val5a", Mng1 = "Mng1a", Mng2 = "Mng2a", Mng3 = "Mng3a",
    Mng4 = "Mng4a", Mng5 = "Mng5a", Mng6 = "Mng6a", Mng7 = "Mng7a", Mng8 = "Mng8a",
    Enact1 = "Enact1a", Enact2 = "Enact2a", Enact3 = "Enact3a", Enact4 = "Enact4a",
    Enact5 = "Enact5a", Enact6 = "Enact6a")

# Second creating a tiny df with just the GroupB observations Add an
# ID variable to each row
IdThreatB <- dplyr::select(idThreatAB, Val1b, Val2b, Val3b, Val4b, Val5b,
    Mng1b, Mng2b, Mng3b, Mng4b, Mng5b, Mng6b, Mng7b, Mng8b, Enact1b, Enact2b,
    Enact3b, Enact4b, Enact5b, Enact6b)
# adding a variable to indicate these are from Group A
IdThreatB$Group <- "GroupB"
# renaming so that when I bind the A and B dfs they have the same
# variable names
IdThreatB <- dplyr::rename(IdThreatB, Val1 = "Val1b", Val2 = "Val2b", Val3 = "Val3b",
    Val4 = "Val4b", Val5 = "Val5b", Mng1 = "Mng1b", Mng2 = "Mng2b", Mng3 = "Mng3b",
    Mng4 = "Mng4b", Mng5 = "Mng5b", Mng6 = "Mng6b", Mng7 = "Mng7b", Mng8 = "Mng8b",
    Enact1 = "Enact1b", Enact2 = "Enact2b", Enact3 = "Enact3b", Enact4 = "Enact4b",
    Enact5 = "Enact5b", Enact6 = "Enact6b")

# Binding the A and B sets of data use this df for the invariance
# homework
IdThreatLONG <- rbind(IdThreatA, IdThreatB)
```

## Anti-Racism Behavioral Inventory 

The Anti-Racism Behavioral Inventory [@pieterse_anti-racism_2022] is a measure that assesses anti-racism awareness and behavior among white Americans. The scale includes 21 items with responses rated on a 5-point Likert scale ranging from 1 (*strongly disagree*) to 5 (*strongly agree*). Higher scores indicate a greater anti-racist awareness and behavior. 

Beneath each of the five factors are a list of the items. Variable names follow in parentheses.

* Individual Advocacy:  
  - When I hear people telling racist jokes and using negative racial stereotypes, I usually confront them (Advoc1)
  - I actively seek to understand how I participate in both intentional and unintentional racism (Advoc2)
  - I actively seek to educate myself about the experience of racism (Advoc3)
  - I interrupt racist conversations and jokes when I heard my friends talking that way (Advoc4)
  - I have challenged acts of racism that I have witnessed in my workplace or at school (Advoc5)
  - I make it a point to educate myself about the experience of historically oppressed groups in the US (e.g. slavery, internment of Japanese, American Indians, and the trail of tears etc.) (Advoc6)
  - I often speak to my friends about the problem of racism in the US, and what we can do about it (Advoc7)
  - I do not like to talk about racism in public (Advoc8) NEEDS REVERSING
  - I interrupt racist conversations and jokes when I hear them in my family (Advoc9)
* Awareness of Racism:  
  - I feel guilty and ashamed when I think of the history of racism and slavery in the US (Aware1)
  - It bothers me that my country has yet to acknowledge the impact of slavery (Aware2)
  - The US should offer some type of payment to the descendants of slaves (Aware3)
  - The US has not acknowledged the impact of slavery (Aware4)
  - Because of racism in the US, Blacks do not have the same educational opportunities as compared to Whites (Aware5)
  - Within the US, racism is largely perpetuated by the White racial majority (Aware6)
  - The police unfairly target Black men and Latinos (Aware7)
* Institutional Advocacy
  - I give money to organizations working against racism and discrimination (Inst1)
  - When I read articles in newspapers or magazines that are perpetuating racist ideas, I generally write a letter to the editor (Inst2)
  - I am actively involved in exposing companies that uphold exclusionary and racist practices (Inst3)
  - I write letters to local and state politicians to voice my concerns about racism (Inst4)
  - I volunteer with anti-racist or racial justice organizations (Inst5)

This article was published in the open access Journal for Social Action in Counseling and Psychology and is available at its [website](https://openjournals.bsu.edu/jsacp/article/view/3679). Below is the script for simulating item-level data from the factor loadings, means, and sample size presented in the published article. 

Four additional scales were reported in the Pieterse et al. [-@pieterse_anti-racism_2022] article. Unfortunately, I could not locate factor loadings for all of them; in these cases, I uniformly assigned the factor loading of 0.8. The scales, their original citation, and information about how I simulated data for each are listed below.

* **White Privilege** was assessed using a 13-item subscale from The Privilege and Oppression Inventory** [@hays_initial_2007]. Items are rated on a Likert scale ranging from 1 (*strongly disagree*) to 6 (*strongly agree*). An example item is, "Whites have the power to exclude other groups." Higher scores indicate greater levels of White privilege.
* **Color Blind Racial Attitudes** [@neville_construction_2000] is a 21-item scale that assesses implicit racism-related attitudes. The 21 items are assessed on a Likert scale ranging from 1 to 5 with higher scores reflecting greater levels of color-blind racial attitudes. I was able to simulate two of the three subscales of the instrument:  Racial Privilege (RP) and Blatant Racial Issues (BR).

Because data is collected at the item level (and I want this resource to be as practical as possible, I have simulated the data for each of the scales at the item level. Simulating the data involved using factor loadings, means, and correlations between the scales. Where possible, factor loadings are retrieved from original (or replication) articles that report on their psychometric evaluation. The means and correlations are from Pietierse et al. [@pieterse_anti-racism_2022] Because the simulation will produce "out-of-bounds" values, the code below rescales the scores into the range of the Likert-type scaling and rounds them to whole values.


```r
#Entering the intercorrelations, means, and standard deviations from the journal article

Antiracism_generating_model <- '
        #measurement model
        ARBI =~ .274*Advoc1 + .699*Advoc2 + .752*Advoc3 + .465*Advoc4 + .479*Advoc5 + .617*Advoc6 + .672*Advoc7 + .455*Advoc8 + .420*Advoc9 + .135*Aware1 + .568*Aware2 + .627*Aware3 + .566*Aware4 + .660*Aware5 + .513*Aware6 + .565*Aware7 + .536*Inst1 + .116*Inst2 + .408*Inst3 + .295*Inst4 + .638*Inst5
        Advocacy  =~ .618*Advoc1 + .055*Advoc2 + .035*Advoc3 + .712*Advoc4 + .275*Advoc5 + .124*Advoc6 + .090*Advoc7 + -.250*Advoc8 + .623*Advoc9
        Awareness =~ .211*Aware1 + .669*Aware2 + .428*Aware3 + .692*Aware4 + .445*Aware5 + .505*Aware6 + .528*Aware7
        Institutional =~ .381*Inst1 + .547*Inst2 + .648*Inst3 + .618*Inst4 + .392*Inst5
        WhitePriv =~ .80*WP1 + .59*WP2 + .62*WP3 + .65*WP4 + .80*WP5 + .50*WP6 + .78*WP7 + .57*WP8 + .64*WP9 + .49*WP10 + .64*WP11 + .61*WP12 + .40*WP13
        CoBRAS_RP =~ .68*RP1 + .66*RP2 + .64*RP3 + .62*RP4 + .62*RP5 + .58*RP6 + .54*RP7
        CoBRAS_BR =~ .77*BR1 + .67*BR2 + .65*BR3 + .65*BR4 + .62*BR5 + .55*BR6 + .48*BR7
        
        #Means
         ARBI ~ 3.91*1
         Advocacy ~5.33*1
         Awareness ~ 4.26*1
         Institutional ~ 1.66*1
         WhitePriv ~ 5.20*1
         CoBRAS_RP ~ 2.54*1
         CoBRAS_BR ~ 1.65*1
         
        #Correlations
         ARBI ~~ .78*Awareness
         ARBI ~~ .87*Advocacy
         ARBI ~~ .75*Institutional
         ARBI ~~ .64*WhitePriv
         ARBI ~~ -.65*CoBRAS_RP
         ARBI ~~ -.60*CoBRAS_BR
         
         Awareness ~~ .50*Advocacy
         Awareness ~~ .34*Institutional
         Awareness ~~ .81*WhitePriv
         Awareness ~~ -.78*CoBRAS_RP
         Awareness ~~ -.62*CoBRAS_BR
         
         Advocacy ~~ .55*Institutional
         Advocacy ~~ .43*WhitePriv
         Advocacy ~~ -.45*CoBRAS_RP
         Advocacy ~~ -.46*CoBRAS_BR

         Institutional ~~ .27*WhitePriv
         Institutional ~~ -.31*CoBRAS_RP
         Institutional ~~ -.34*CoBRAS_BR
         
         WhitePriv ~~ -.85*CoBRAS_RP
         WhitePriv ~~ -.6*CoBRAS_BR
         
         CoBRAS_RP ~~ .60*CoBRAS_BR
         '
         
set.seed(240218)
AntiR <- lavaan::simulateData(model = Antiracism_generating_model,
                              model.type = "sem",
                              meanstructure = T,
                              sample.nobs=153,
                              standardized=FALSE)

#used to retrieve column indices used in the rescaling script below
col_index <- as.data.frame(colnames(AntiR))

#The code below loops through each column of the dataframe and assigns the scaling accordingly
#Rows 1 thru 21 are the ARBI 
#Rows 22 thru 34 are the White Privilege Scale
#Rows 35 thru 48 are the CoBRAS


for(i in 1:ncol(AntiR)){  
  if(i >= 1 & i <= 21){   
    AntiR[,i] <- scales::rescale(AntiR[,i], c(1, 5))
  }
    if(i >= 22 & i <= 34){   
    AntiR[,i] <- scales::rescale(AntiR[,i], c(1, 6))
    }
      if(i >= 35 & i <= 48){  
    AntiR[,i] <- scales::rescale(AntiR[,i], c(1, 5))
      }
}

#rounding to integers so that the data resembles that which was collected
library(tidyverse)
AntiR <- AntiR %>% round(0) 

#quick check of my work
#psych::describe(AntiR) 

#Reversing the supportive item on the Perceptions of LGBTQ Campus Climate Scale so that the exercises will be consistent with the format in which the data was collected
```

The optional script below will let you save the simulated data to your computing environment as either an .rds object (preserves any formatting you might do)  or a.csv file (think "Excel lite").


```r
# to save the df as an .rds (think 'R object') file on your computer;
# it should save in the same file as the .rmd file you are working
# with saveRDS(AntiR, 'AntiR.rds') bring back the simulated dat from
# an .rds file AntiR <- readRDS('AntiR.rds')
```


```r
# write the simulated data as a .csv write.table(AntiR,
# file='AntiR.csv', sep=',', col.names=TRUE, row.names=FALSE) bring
# back the simulated dat from a .csv file AntiR <-
# read.csv('AntiR.csv', header = TRUE)
```

Lessons in this volume teach test-retest reliability and invariance testing. In both of these circumstances, data from two different administrations of the focal test are required. For test-retest, these would be completed by the same person; for invariance-testing, these would be completed by different people. Below I have simulated two sets of data for the Anti-Racism Behavioral Inventory [@pieterse_anti-racism_2022]. I have named them "A" and "B". For your homework purposes, you can determine if they will represent testing with the same individual (appropriate for test-retest reliability) or different groups (appropriate for invariance testing).

The Pieterse et al.[-@pieterse_anti-racism_2022] article did not report invariance testing nor test-retest reliabilities. Therefore, I simulated this data following the general patterns of such testing.


```r
ARBI_generating_modelAB <- '
        #measurement model
        AdvocacyA  =~ .450*Advoc1a + .671*Advoc2a + .715*Advoc3a + .650*Advoc4a + .548*Advoc5a + .634*Advoc6a + .593*Advoc7a + .532*Advoc8a + .592*Advoc9a
        AwarenessA =~ .239*Aware1a + .836*Aware2a + .754*Aware3a + .877*Aware4a + .791*Aware5a + .727*Aware6a + .782*Aware7a
        InstitutionalA =~ .698*Inst1a + .397*Inst2a + .680*Inst3a + .589*Inst4a + .798*Inst5a2293*Advoc7b + 532*Advoc8b + .564*Advoc9b
        AdvocacyB =~ .378*Advoc1b + .666*Advoc2b + .683*Advoc3b + .555*Advoc4b + .672*Advoc5b + .822*Advoc6b + .511*Advoc7b + .488*Advoc8b + .513*Advoc9b
        AwarenessB =~ .253*Aware1b + .800*Aware2b + .721*Aware3b + .842*Aware4b + .701*Aware5b + .797*Aware6b + .742*Aware7b
        InstitutionalB =~ .623*Inst1b + .301*Inst2b + .666*Inst3b + .533*Inst4b + .721*Inst5b

        #Means
         AdvocacyA ~5.33*1
         AwarenessA ~ 4.26*1
         InstitutionalA ~ 1.66*1
         AdvocacyB ~5.25*1
         AwarenessB ~ 4.30*1
         InstitutionalB ~ 1.71*1
         
         
         #Correlations
         AdvocacyA ~~ .80*AwarenessA
         AdvocacyA ~~ .80*InstitutionalA
         AdvocacyA ~~ .63*AdvocacyB
         AdvocacyA ~~ .57*AwarenessB
         AdvocacyA ~~ .56*InstitutionalB
         
         AwarenessA ~~ .77*InstitutionalA
         AwarenessA ~~ .59*AdvocacyB
         AwarenessA ~~ .70*AwarenessB
         AwarenessA ~~ .58*InstitutionalB
         
         InstitutionalA ~~ .54*AdvocacyB
         InstitutionalA ~~ .79*AwarenessB
         InstitutionalA ~~ .66*InstitutionalB
         
         AdvocacyB ~~ .81*AwarenessB
         AdvocacyB ~~ .82*InstitutionalB
         
         AwarenessB ~~ .81*InstitutionalB
        
         '

set.seed(240326)
ARBI_AB <- lavaan::simulateData(model = ARBI_generating_modelAB,
                              model.type = "sem",
                              meanstructure = T,
                              sample.nobs=300,
                              standardized=FALSE)

#used to retrieve column indices used in the rescaling script below
col_index <- as.data.frame(colnames(ARBI_AB))

#The code below loops through each column of the dataframe and assigns the scaling accordingly
#All rows are the iBel scales, administrations A and B


for(i in 1:ncol(ARBI_AB)){  
  if(i >= 1 & i <= 42){   
    ARBI_AB[,i] <- scales::rescale(ARBI_AB[,i], c(1, 5))
  }
}

#rounding to integers so that the data resembles that which was collected
library(tidyverse)
ARBI_AB <- ARBI_AB %>% round(0) 

#quick check of my work
#psych::describe(iBelAB) 
```

If you want to use the data for invariance testing, the data will need to be in *long* form. Here's code to get it there. 


```r
# First creating a tiny df with just the GroupA observations Add an
# ID variable to each row
ARBI_A <- dplyr::select(ARBI_AB, Advoc1a, Advoc2a, Advoc3a, Advoc4a, Advoc5a,
    Advoc6a, Advoc7a, Advoc8a, Advoc9a, Aware1a, Aware2a, Aware3a, Aware4a,
    Aware5a, Aware6a, Aware7a, Inst1a, Inst2a, Inst3a, Inst4a)
# adding a variable to indicate these are from Group A
ARBI_A$Group <- "GroupA"
# renaming so that when I bind the A and B dfs they have the same
# variable names
ARBI_A <- dplyr::rename(ARBI_A, Advoc1 = "Advoc1a", Advoc2 = "Advoc2a",
    Advoc3 = "Advoc3a", Advoc4 = "Advoc4a", Advoc5 = "Advoc5a", Advoc6 = "Advoc6a",
    Advoc7 = "Advoc7a", Advoc8 = "Advoc8a", Advoc9 = "Advoc9a", Aware1 = "Aware1a",
    Aware2 = "Aware2a", Aware3 = "Aware3a", Aware4 = "Aware4a", Aware5 = "Aware5a",
    Aware6 = "Aware6a", Aware7 = "Aware7a", Inst1 = "Inst1a", Inst2 = "Inst2a",
    Inst3 = "Inst3a", Inst4 = "Inst4a")

# Second creating a tiny df with just the GroupB observations Add an
# ID variable to each row
ARBI_B <- dplyr::select(ARBI_AB, Advoc1b, Advoc2b, Advoc3b, Advoc4b, Advoc5b,
    Advoc6b, Advoc7b, Advoc8b, Advoc9b, Aware1b, Aware2b, Aware3b, Aware4b,
    Aware5b, Aware6b, Aware7b, Inst1b, Inst2b, Inst3b, Inst4b)
# adding a variable to indicate these are from Group A
ARBI_B$Group <- "GroupB"
# renaming so that when I bind the A and B dfs they have the same
# variable names
ARBI_B <- dplyr::rename(ARBI_B, Advoc1 = "Advoc1b", Advoc2 = "Advoc2b",
    Advoc3 = "Advoc3b", Advoc4 = "Advoc4b", Advoc5 = "Advoc5b", Advoc6 = "Advoc6b",
    Advoc7 = "Advoc7b", Advoc8 = "Advoc8b", Advoc9 = "Advoc9b", Aware1 = "Aware1b",
    Aware2 = "Aware2b", Aware3 = "Aware3b", Aware4 = "Aware4b", Aware5 = "Aware5b",
    Aware6 = "Aware6b", Aware7 = "Aware7b", Inst1 = "Inst1b", Inst2 = "Inst2b",
    Inst3 = "Inst3b", Inst4 = "Inst4b")

# Binding the A and B sets of data use this df for the invariance
# homework
ARBI_long <- rbind(ARBI_A, ARBI_B)
```
