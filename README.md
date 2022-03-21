# 2021D4GC

## Opening words
Welcome to the **2021 Data 4 Good Challenge (D4GC)** documentation. My name is **[Gunho Lee](https://www.linkedin.com/in/gunho-lee/)**, who was the Lead D4GC challenge design. Before diving into the details, I would like to first send massive thanks to the entire **[Emergent team](https://www.linkedin.com/company/emergent-leuven)**, and especially **[Saptarshi Chakrabarti](https://www.linkedin.com/in/csap96/)** and **[Juli Dema](https://www.linkedin.com/in/julidema/)**, who worked on it together with me.

The purpose of this document is to summarize the journey to **the 2021 D4GC** and provide self-feedback to ourselves that would be useful for the next D4GC challenge design.

The document will consist of mainly three parts:
- **Strategical data brain-storming**
- **Technical data build-up**
- **Challenges within the challenge design**
- **Lessons during the journey**

## Strategical data brain-storming
Brain-storming is essential in most group works. Especially for the D4GC, a specific process, so-called DATA brain-storm (according to me), is highly needed. Precisely, we adopted a **Top-Down approach**, meaning that we started with identifying the broader concept of the challenge first and narrow down the options.

Within this framework, the team arrived at the following motivation *"We will tackle one of the prevalent major problems (social issues) on earth".*

What follows was to put every interesting social issue into one basket before sorting them out. The shared issues were as follows:  
**1. Mental health**
**2. Plastic pollution**
**3. Environmental crisis (temperature, etc)**
**4. Economical issues**

The uttermost question of the team during the design process was *"How do we apply DATA for such issues?"*. Put differently, it was essential to carefully consider the followings:  
- Do we have **enough data** to solve the issue?
- Are data **reliable**?
- **What can you do** with this data?
- Can you create **technical aspects out of data** while allowing non-technical students to interpret the data?

D4GC stands out from the peer challenges since it opens the chance to not only technical students but also non-technical ones. In other words, we believe data requires a technical mindset as well entrepreneurial insight. Therefore, it is crucial for the challenge design team to aim to balance these two main aspects. This should be properly addressed at the beginning stage.

## Technical data build-up
In this section, I will focus on the data manipulation and specific methods that we utilized instead of explaining the sources of the original datasets. If necessary, please check out the links that are added next to the keywords.

**1. Dataset 1 & 2**
IPCC. 

**2. Dataset 3 & 4**  
Dataset 3 provides demographic indicators such as Population (+ growth rate) and GDP per capita, while Dataset 4 shows energy consumption (co2, overall consumption per capita) of the countries. The original data are from multiple databases which are internationally recognized, which can be found in the reference page of **[the challenge documentation](https://github.com/nopps07/2021D4GC/blob/main/2021%20D4GC%20Challenge%20Documentation.pdf)**.  

In order to complete these datasets, the following steps were taken:  
  - Select indicators that are relevant to the topic.
  - Preprocess the data.

Note that the data preprocessing should normally contain *dealing with missing data* and *normalization*. Some countries are more likely to have missing data as they would not have enough data channels to report, whereas most developed countries do not have any missing values. In addition, it was crucial to keep in mind that the different units and measurements were utilized as they are from multiple databases. The latter was clearly managed during the process. But, the missing data was not clearly handled in the process due to the following reason:
  - We would not exclude countries just because they do not have enough data. (Avoiding the case that people only work on developed countries + minimize bias)  
 
Despite our acceptable intention, it would have created better outcomes if the participants had not had to spend time dealing with missing data. Note that **Select & Focus** is always essential in many ways.

**3. Dataset 5 (ISSP Survey)**  
The original data is *[the international Social Survey Programme 2010 - Environment III](http://www.issp.org/menu-top/home/)*. As our challenge highlited on the environmental concern. It was important to collect a survey which could reflect how citizens percieve prevalent environmental issues. The taken steps in order to arrive *Dataset 5* are as follows:  
  - Select relevant survey questionnaires (ex: environmental-friendly behaviour (quantitative) + macro-indicators: Education level, income group (qualitative))  
  - Combine similar questionnaires to one so it has larger and clearer distribution.  
  - In order to perform this summation, the *Cronbach's Alpha* parameter was obtained. In general, the parameter larger than 0.7 is considered good and therefore those questionnaries can be merged. Our criteria was to have larger than 0.75 in order to increase validity. The example codes can be found below  
```
library(dplyr)
library(ltm) #cronbach alpha

#Import raw data
#Note that we already have selected relevant questionaires
issp <- read.csv("ISSPtrial.csv", header = TRUE)

#Cronbach's alpha (example)
df <- issp %>% dplyr::select(v39:v45)
df <- df %>% 
  na.omit()
cronbach.alpha(df) # 0.816; interpretation: Climate change is extremely dangerous for the environment

#Manipulation
#1. Delete missing data (not recommend in pratice)
#2. Change Likert Scale to more intuitive order (6 = Most, 1 = Least)
#3. Combine 
df <- df %>%
  na.omit() %>%
  mutate(v29 = 6 - v29, v30 = 6 - v30, v31 = 6 - v31, v32 = 6 - v32, v33 = 6 - v33,#care_env
         v34 = 6 - v34, v35 = 6 - v35, v36 = 6 - v36, #exag_env
         v39 = 6 - v39, v40 = 6 - v40, v41 = 6 - v41, v42 = 6 - v42, v43 = 6 - v43, v44 = 6 - v44, v45 = 6 - v45, #climate_crisis
         v58 = 5 - v58, v59 = 5 - v59, v60 = 5 - v60, #protect_env
         gov_peo = v46,
         gov_bus = v47,
         how_bus = v49,
         how_peo = v50,
         mem_env = v61,
  ) %>%
  mutate(care_env = v15 + v29 + v30 + v31 + v32 + v33 + v38,
         exag_env = v34 + v35 + v36,
         climate_crisis = v39 + v40 + v41 + v42 + v43 + v44 + v45,
         protect_env = v58 + v59 + v60)
#Note that the merging process is verified by larger than 0.75 Cronbach alpha
```

The possible actions that the D4GC participants could have taken were:  
  - Regression analysis: does income level or educational achievement affect your attitude towards environmental issues?
  - Cluster analysis: can we find out the certain clusters from the countries? If so, what makes them different?

## Challenges within the challenge design
PROBLEMS  
1. Large-Sized Data  
Importing data was already a big challenge as it requires an extensive memory of your computer. It also took a lot of minutes just to get your data ready in your working environment. What we could have done would be using PyArrow instead of Pandas. Check *[this article](https://medium.com/towards-data-science/stop-using-pandas-to-read-write-data-this-alternative-is-7-times-faster-893301633475)* for more information 
		
2. Geodata
a. this could be the biggest challenge we faced. The dataset was high-dimensional, and it was sorted by latitude and longitude which needed to be converted into corresponding places. 
b. We have found a number of possible solutions which include APIs, however, none of them worked in a way we would need desperately.
The worked solution: geo package in R 

```
library(maps)

GISCONVERT <- function(df) {
  	start <- Sys.time()
  	country <- map.where(database = "world",
            	df$lon, df$lat)
  	endm <- Sys.time
  	country_df <- as.data.frame(country)
  	new_df <- rbind(df, country_df)
	}
```
*Note*: After GISCONVERT, you need to manipulate and tidy your data frame. In this post, I skip those parts as they are not in the main focus.
