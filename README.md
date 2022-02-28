# 2021D4GC

## Opening words
The purpose of this document is to summarize the journey to the 2021 Data 4 Good Challenge and provide self-feedback to ourselves that would be useful for next D4GC challenges.

My name is Gunho Lee, who took the position of Lead D4GC challenge, and I would like to send massive thanks to the entire Emergent team, especially to the Executive Board, Rishi and Juli who had been hard working together.

The document will consist of mainly three parts:
- Strategical data brain-storming
- Technical data build-up
- Challenges within the challenge
- Lessons during the journey

## Strategical data brain-storming
Brain-storming is essential in most group works. Especially for the D4GC a specific process, so-called DATA brain-storm (according to me), is highly needed. In detail, we adopted a Top-Down approach from the beginning, meaning that we started with identifying the broader concept of the challenge.

Within this framework, the first accordance at which the team arrived was, in a simpler way, to solve one of the prevalent major problems on earth.

What follows was to put every interesting issue into one basket before sorting them out. The shared issues were as follows:  
1. Mental health
2. Plastic pollution
3. Environmental crisis (temperature, etc)
4. Economical issues

From my side, the uttermost question during the design process had been 'How do we apply DATA for such issues?'. In other words, it was essential to carefully consider the followings:
	- Do we have enough data to solve the issue?
	- Are data reliable?
	- What can you come up with this data?
  - Can you create technical aspects out of data?


## Challenges within the challenge
PROBLEMS  
1. working with large data importing data was already a big challenge as it requires an extensive memory of your computer. It also took a lot of minutes just to get your data ready in your working environment. What we could have done would be using PyArrow instead of Pandas. Check this article for more information https://medium.com/towards-data-science/stop-using-pandas-to-read-write-data-this-alternative-is-7-times-faster-893301633475
		
2. Geodata
a. this could be the biggest challenge we faced. The dataset was high-dimensional, and it was sorted by latitude and longitude which needed to be converted into corresponding places. 
b. We have found a number of possible solutions which include APIs, however, none of them worked in a way we would need desperately.
The worked solution: geo package in R 

