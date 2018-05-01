## Books/Articles/Papers/Tools
* Articles
    * [Twitter and social network analysis](http://datadrivenjournalism.net/news_and_analysis/twitter_and_social_network_analysis)
    * [Esempio di utilizzo di gephy e twitter su referendum ed influencer](http://www.misurarelacomunicazione.it/2016/11/24/iovotono-vs-bastaunsi-gli-influencers-twitter/)
    * [Social network analysis of Twitter](http://www.mediative.com/social-network-analysis-twitter/)
    * [Data Mining for Predictive Social Network Analysis](https://www.toptal.com/data-science/social-network-data-mining-for-predictive-analysis)
    * [Network analysis on Clinton Wikileaks data, by MIT](https://clinton.media.mit.edu/clinton#)
    * [A social network analysis of Twitter: Mapping the digital humanities community](https://www.tandfonline.com/doi/full/10.1080/23311983.2016.1171458) 
    * [Articolo analisi su \#deletefacebook in Italia](https://socialrecap.it/2018/03/26/deletefacebook-ci-credono-media-non-gli-italiani/)
    
* Papers 
    * [Classifying Twitter Topic-Networks Using Social Network Analysis](http://journals.sagepub.com/doi/full/10.1177/2056305117691545)
    * [Towards More Systematic Twitter Analysis: Metrics for Tweeting Activities](https://www.researchgate.net/publication/235632738_Towards_More_Systematic_Twitter_Analysis_Metrics_for_Tweeting_Activities)
    * [The Anatomy of a Scientific Rumor (Higgs boson on twitter)](https://www.nature.com/articles/srep02980#methods), qua il [dataset](https://snap.stanford.edu/data/higgs-twitter.html)

* Books
    * [Mastering Social Media Mining with Python](https://www.amazon.it/Mastering-Social-Media-Mining-Python/dp/1783552018/ref=sr_1_1?ie=UTF8&qid=1521482811&sr=8-1&keywords=Mastering+Social+Media+Mining+with+Python)

* Tools
    * [Twitter's Search Bar](https://twitter.com/search-home)
    * [Network repository](http://networkrepository.com/)
    * [Hashtagify](http://hashtagify.me/hashtag/deletefacebook)


## Possible Topics

* DataScience 
    * \#datascience \#AI ...
    * \#facebookgate \#CambridgeAnalytica \#Zuckerberg \#deletefacebook
    * \#privacy \#GDPR

* Politics  
    * Elections
    * Parties
    * Single politicians

* Communities
    * Software communities
    * Town/cities
    * 

* Music

* Brands

* People
    * Popular public persons


## Various
Let's begin thinking about quantities.

Full size of a tweet: ~2KB [link to measure the size of a tweet](https://gist.github.com/brendano/1024217)
to be checked, storing in json format?

* How many tweets can we store easily?
    * 100K  tweets  ~200MB
    * 500K  tweets  ~1GB
    * 1M    tweets  ~2GB
* How much time to build the network? 

* Stream rate?
The maximum stream rate for the twitter API is 450 GET REQUEST for 15minutes. Each request can contain 100 tweets. So the maximum rate is:
MAX_RATE = 45000 tweet/15minuti = 45000/900sec = 50 tweet/s.
To respect this rate I've put to sleep the script every 500 tweets for 12 sec, obtaining :
RATE = 500/12 = 41 tweet/s
Fundamental is to use the COUNT=100 option in the search, to not deplete the admitted requests too quickly, killing down the rate.

Maybe 12 seconds of sleep is too much conservative:

Time for 45000 tweet: 12seconds * 45000tweet / 500 = 12*90 = 1080 s =18minutes

We lose theoretically 3 minutes every 15 minutes: 12 minutes for hour.

In reality I'm going with a much slower rate:

Now, 'Tue Mar 27 23:58:56 2018', 45000/30minutes = 25 tweets/sec
Half of the maximum rate speed.
We have also to consider the time for requests/writing to file/zipping.



* How many tweets have already been tweeted about for example \#deletefacebook?

Consideration: since, as seen [here](https://gist.github.com/brendano/1024217), tweets are represented in a dictionary-like data structure, we only have to store the key-value couples that are meaningful for our pourposes. Having a network that has users for nodes and tweets/retweets for links, we only need to store users IDs and infos on the connections between the tweets. However it may be very useful to take a look about all the metadata that comes with a single tweet, in order to see which of the various fields may be used to obtain a richer analysis. Having choosen the kind of infos we want to store, using a compression algorithm like gzip or similar should make the task of storing the data a bit simpler.