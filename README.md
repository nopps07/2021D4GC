# 2021D4GC

## Opening words
Welcome to the 2021 Data 4 Good Challenge (D4GC) documentation. My name is Gunho Lee, who took the position of Lead D4GC challenge design, and I would like to send massive thanks to the entire Emergent team, and especially Rishi and Juli, who had been hard working on it together.

The purpose of this document is to summarize the journey to the 2021 Data 4 Good Challenge and provide self-feedback to ourselves that would be useful for the next D4GC challenge design.

The document will consist of mainly three parts:
- Strategical data brain-storming
- Technical data build-up
- Challenges within the challenge design
- Lessons during the journey

## Strategical data brain-storming
Brain-storming is essential in most group works. Especially for the D4GC a specific process, so-called DATA brain-storm (according to me), is highly needed. In detail, we adopted a Top-Down approach from the beginning, meaning that we started with identifying the broader concept of the challenge.

Within this framework, the first accordance at which the team arrived was, in a simpler way, to solve one of the prevalent major problems on earth.

What follows was to put every interesting issue into one basket before sorting them out. The shared issues were as follows:  
1. Mental health
2. Plastic pollution
3. Environmental crisis (temperature, etc)
4. Economical issues

For the team, the uttermost question during the design process was 'How do we apply DATA for such issues?'. In other words, it was essential to carefully consider the followings:  
- Do we have enough data to solve the issue?
- Are data reliable?
- What can you come up with this data?
- Can you create technical aspects out of data?

D4GC stands out from the peer challenges since it comes with not only technology but also a business. In other words, we believe data requires a technical mindset as well entrepreneurial insight. Therefore, it is crucial for the challenge design team to aim to balance these two main aspects. 

## Technical data build-up
In this section, I am not going to explain in detail where the original datasets came from. Instead, I will focus on the data manipulation and specific methods that we utilized.

1. Dataset 1 & 2
IPCC. 

2. Dataset 3 & 4

3. Dataset 5 (ISSP Survey)
The original data is *the international Social Survey Programme 2010 - Environment III*. As our challenge highlited on the environmental concern. It was important to collect a survey which could reflect how citizens percieve prevalent environmental issues. The taken steps in order to arrive *Dataset 5* are as follows:  
a. Select relevant survey questionnaires (ex: environmental-friendly behaviour (quantitative) + macro-indicators: Education level, income group (qualitative))  
b. Combine similar questionnaires to one so it has larger and clearer distribution.  
In order to perform this summation, the *Cronbach's Alpha* parameter was obtained. In general, the parameter larger than 0.7 is considered good and therefore those questionnaries can be merged. Our criteria was to have larger than 0.75 in order to increase validity.  

The possible actions that the D4GC participants could have taken were:  
- Regression analysis: does income level or educational achievement affect your attitude towards environmental issues?
- Cluster analysis: can we find out the certain clusters from the countries? If so, what makes them different?

## Challenges within the challenge design
PROBLEMS  
1. Large-Sized Data  
Importing data was already a big challenge as it requires an extensive memory of your computer. It also took a lot of minutes just to get your data ready in your working environment. What we could have done would be using PyArrow instead of Pandas. Check this article for more information https://medium.com/towards-data-science/stop-using-pandas-to-read-write-data-this-alternative-is-7-times-faster-893301633475
		
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
