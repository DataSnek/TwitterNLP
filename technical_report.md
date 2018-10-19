

## Problem Statment
Social media is such a large landscape these days that it’s hard to get a grasp on exactly how big of a footprint it has grown into. [Twitter](https://twitter.com/) users in 2010 had a very different experience than they do today because the number of users has grown ten fold to 300 million since then. It is now a staple of promotion and marketing as well as being a social media site. There is a short list of people including Jennifer Lawerence, Emma Thompson and George Clooney that do not use Twitter but overall anyone who is anyone has an account. This includes corporations and government entities. Never before has there been so much self reported data. For this project my goal is to be able to gain insight about what people are saying and who they are saying it too using unsupervised learning and network visualizations. Topic modeling is useful when there is not an understanding of the grouping or topics of text. Twitter data is an opportunity to reveal patterns and connections the would be simply impossible to do for humans. While we may be able to relate to individual topics and themes there is a huge barrier to overall understanding posed by 300,000 short text bodies. My goal is to make the themes and interactions clearer all starting with a single user account. The commercial/promotional implications of such an analysis is not directly stated but implied. 

## Data Collection


Tweets were pulled from the [Twitter API](https://developer.twitter.com/) based on username using the [Tweepy](http://www.tweepy.org/) package. Access to the Twitter API is granted through a [developer account](https://developer.twitter.com/en/apply-for-access.html) which requires writing a 300 word statement on intended use. As a starting point I choose a journalist that I know little about other than he works [WIRED](https://www.wired.com/) magazine. After looking at ~3200 tweets I take the 100 top mentions from the individuals account and collect those tweets for a total of ~320,000 individual communications. All of the information gathered for network analysis was taken from the text body in relation to it’s author. Some accounts do not allow their Tweets to be viewed and beacuse of this only 57/100 of the accounts were collected.

## Exploratory Data Analysis 

Tweets from the central user’s account were collected and a frequency chart gives us a sense of his comment distribution. His number one mention is WIRED which is his employer. The second is another wired journalist. 

![User Mentions Frequency Distribution](https://github.com/DataSnek/TwitterNLP/blob/master/Pics/freq1.png)

Looking at a sample of distributions from a sample of top mentions you can start to get a sense of the social network becasue almost all of them mention at least 3 of the other users.

![Connected User Mentions Frequency Distribution](https://github.com/DataSnek/TwitterNLP/blob/master/Pics/freq2.png)

Looking at the data it becomes clear that the theme of every tweet can be very different. The first result is FaceBook and the second is Formula One racing. Trends in thousand of tweets would not be viewable but through topic modeling we can gain valuable insight.
From the top 100 mentions the corpus was collected and Tweet is decomposed into vectors to represent the words frequency and distribution. The vectorization is not related to the network graph but the information is extracted 

![Sample of Tweets](https://github.com/DataSnek/TwitterNLP/blob/master/Pics/tweets.png)

## Network Analysis

At this point we have collected the names and frequencies of mentions between accounts allowing a visualization of the interconnectivity. The central user is in the middle and the most connected point is WIRED. This is show here with a spring [NetworkX](https://networkx.github.io/) spring graph. 

![NetworkX Spring Graph](https://github.com/DataSnek/TwitterNLP/blob/master/Pics/spring.png)

While this is useful a force directed ego graph is cleaner and more useful. The most influential people are the ones most connected. Note Selina Gomez is on the outer circle while Hilary Clinton is one of the most influential people in this particular network. Unsurprisingly WIRED is the most influencial. You can see that there is a huge amount of connectivity in this network. Unfortunately to really appreciate and see  larger network connectivity graph it requires a very large monitor which I used during this project. 

![NetworkX Force Directed Ego Graph](https://github.com/DataSnek/TwitterNLP/blob/master/Pics/force_ego.png)

## Unsupervised Clustering for Topic Analysis

In order to be able to see the data a dimensionality reduction is performed using t-distributed stochastic neighbor embedding(t-SNE). It is a 2D representation of a multi-dimensional dataset. These are especially unique looking users I picked from the first 20 users in the list. The unique shape of each plot gives us abstract information about how this person directs and words their comments. Small outer clusters represent very unique topics. The result is like a person’s Twitter finger print. This method is helpful in a qualitative sense but the calculations involved in the dimensionality reduction for t-SNE are so costly that it was not run on the entire set of user tweets. 


![t-SNE t](https://github.com/DataSnek/TwitterNLP/blob/master/Pics/tSNE.png)

Individual user tweets are being grouped into clusters indicating there are some distinct topics they are Tweeting about. Each user has a unique Tweet "fingerprint" and the right middle graph has a suspiciously uniform distribution of Tweets potentially indicating an automated account.
This analysis while interesting does not tell us what these topics are in a context of the entire social group. To do his we need to use Latent Dirichlet allocation on the entire body of Tweets. Doing so returns the following topics:

`Topic #0: just think right today america trump going know laurenduca don friends nxthompson gun eagles make really cnn wants people sorry`

Clearly we can see that there are distict topics. However not all of them are discernable. But not all is lost becasue turning to google gives us a clear understanding of the topic. For Topic #0 the results are clearly the author Lauren Duca discussing trump. 

![topic0](https://github.com/DataSnek/TwitterNLP/blob/master/Pics/topic0.png)

`Topic #1: wired read like thing story important want woman today news new real right fake did things cover trump know thought`

Even when the search results do not converge you can see that Topic #1 is simply WIRED magazine.

![topic1](https://github.com/DataSnek/TwitterNLP/blob/master/Pics/topic1.png)
 
`Topic #2: trump just like man day sure dr san francisco don let hope good going today know new time social tweets`

Topic #2 is more vauge but centered around Trump. 

`Topic #3: zuckerberg mark thanks like facebook need news don trump make does twitter lucky know actually wired good feel got president`

Topic #3 is FaceBook and Mark Zuckerberg.

`Topic #4: ve best time pardesoteric ll know love don life come world snackfight wired happy read things good think facebook let`

Topic #4 is SF author Michael Calore

`Topic #5: people don facebook trump zuckerberg today just live make wired realdonaldtrump problems mark told new guys forget think going man`

Topcic #5 is also FaceBook and Mark Zuckerberg

`Topic #6: yes time people right just think wired year trump did like said today 2017 world don news old president lying`
 
 Topic #6 is politics. You can see that there is some subjectivity to the analysis but overall we are resolving well. The number of topics is decided beforehand. 10 topics gave the optimum resolve when compared to 5,20 and 30. 

`Topic #7: wired reading people know thanks thank trump twitter president years ve glad words today man don hope kind john best`

`Topic #9: hey did trump na day kavanaugh news right best people facebook isn brett ll fine president thing got want aren`


## Conclusion

The amount of information that is accessible through unsupervised modeling of topics in text  depends on the type of information you feed into it. When looking at Tweets, some Twitter accounts are much less resolvable than others or require different parameters or models. The endpoints of unsupervised models are not as hard as other ML tasks but a characterized model’s ability to sort many documents quickly far outpaces a human. Some of the distributed topics are actually almost impossible for a person to identify while vector representation and unsupervised clustering can identify connections. 

## Additional Work

In addition to this study an investigation into larger network structures and the distribution of the topics discussed is proposed. Determining a way to spread the search from user to user around a central group could be achieved by setting node parameters for the number of connections and a centrality score. Also building up a Twitter account would allow me to set up some automated interactions using NLP and my profile. I want to have a chatbot that you can request network info from.

