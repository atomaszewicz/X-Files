# The X-Files

For those not familiar with the *The X-Files*, it is a 90s science-fiction show (with a 10th season revival in 2016) with a wonderfully spooky atmosphere (filmed in Vancouver for first 5 seasons) where two FBI agents study alien conspiracies and other paranormal activity. It stars David Duchovny as FBI agent Fox "Spooky" Mulder, an alien conspiracy theorist, and his skeptical partner Doctor Dana Scully, played by Gillian Anderson, as they study unexplained or overlooked cases called 'X-Files'. Scully, with her scientific background and analytical mindset, was assigned to work with Mulder in an effort to debunk his obsessive work studying these cases. However, the longer Scully works with Mulder, the more high-ranking government agents get in the way of her and Mulder's investigations, and the more she begins to believe that there might be a government cover-up... of something.

In the X-Files there are 2 types of episodes: those that feature Mulder and Scully investigating the series-arcing alien conspiracy known as *mytharc* shows, and those that are one-off 'X-Files', often referred to as *Monster of the Week* episodes. The goal of this project is to compare how these two types of episodes compare, and ultimately find out which one is better.

## Two Episodes to Contain Them All

X-Files is not unique in the sense that it has episodes that are self-contained and others that contribute to the series-long plot, but the ability to distinguish between these is considerably easier than in most shows. However it is still imperfect, as sometimes elements of the government conspiracy bleed into *Monster of the Week* (MotW) episodes, and vice-versa. After straining my personal knowledge and memory of the show I decided to work with the classifications done by the phenomenal website http://www.insidethex.co.uk (they have transcribed every episode of the show by-hand!). Their method is to classify episodes as 'mytharc' only if they directly feature elements of the government conspiracy <sup> [1] </sup>. This leans towards more episodes being classified as *MotW* than other methods, but to me it is the most objective way it can be done.

## Data

As in my previous projects I use IMDb's [user ratings of episodes](http://www.imdb.com/title/tt0106179/epdate?ref_=ttep_ql_3). I chose IMDb mainly because of it's large population of voters (average of over 2000 per episode of The X-Files). There are indeed other sites where users can rate episodes of tv shows, but without a large community, they are more susceptible to vote-rigging, and thus the ratings are less trustworthy.

The only other big decision for this project is whether or not to include the 10th season revival from 2016. With the series creator and executive producer Chris Carter back on the series along with some of the main writers and other staff <sup> [2] </sup> <sup> [3] </sup> I was tempted to include the 10th season in my analysis, but I believe that still too much time has passed, and too much has changed from the original airing for it to be compared. Sure enough, upon preliminary analysis of the 6-episode revival season, the episode were significantly lower, didn't adhere to certain trends that the other 9 seasons did, and with only 6 episodes didn't lead to much insight. Therefore I chose to only include seasons 1-9 of the original airing in my analysis.

## First Look

The X-Files average and median episode score is 8.1/10 with a standard deviation of 0.7, with the highest and lowest rated episodes scoring 9.4 and 6.0 respectively. There are 125 *motw* shows, which average a score of 7.8, and 76 *mytharc* episodes which average 8.5. So the *mytharc* episodes are a little above average, and the *monster* episodes a little below. 

![rate_box_jitter](https://raw.githubusercontent.com/atomaszewicz/X-Files/master/RStudio/Plots/rate_box_jitter.png)

## Seasons change...

Not a single season has average *mytharc* shows finishing behind average *motw* shows. Though I like the alien conspiracy episodes more in general, towards the end of the series they get a little disjointed, outlandish, and confusing (yes, even for a show about monsters and aliens). This difference isn't nominal either, two thirds of the seasons see the two episode types ratings split by over 0.6 points.

All but the final season's *mytharc* ratings are above the series' average score of 8.1, and only two season's *motw* scores are above this average.

![season_avg_type](https://raw.githubusercontent.com/atomaszewicz/X-Files/master/RStudio/Plots/season_avg_type.png?raw=TRUE)


## A Little of Column A, a Little of Column B

Next we want to look at how the ratings change when one shifts between episode types.

Throughout the series the the episode type changes 36 times each, NN 39 times, and YY 89 times. Though there are 125 *motw* and 76 *mytharc*, it is still surprising how few NN occurances there are, but it shows that 50% of *mytharc* episodes are sandwiched between two *motw* episodes.

Unsuprsingly the difference in score between episodes of the same type are very small. When there are back-to back *mytharc* or *motw* the median difference is 0, and average difference is -0.09 and -0.04 respectively. It is interesting that they are both negative, but since we are adding many positive and negative values it is likely not significant.

When the episode type changes, our previous result is reinforced: the *mytharc* shows are more popular than the *motw* ones. When going from *motw* to *mytharc* the score raises by an average 0.6 points, and going in the other direction the score drops a bit, by an average -0.4 points. 


## Regions change...

There's one last thing I'd like to know: is my favoritism for the seasons filmed in Vancouver just a love of my own hometown or is there something to the Canadian episodes that make them better?

As all my Vancouverite friends agree, the show seems to have lost something when it moved from filming in Vancouver to filming in LA between season 5 and 6. Not only could we no longer play the 'where was this filmed?' game, but more importantly the misty, eerie, pine-tree laden man-vs-nature atmosphere of the Pacific Northwest was gone. It was likely no mistake that when they brought the show back two years ago, they decided to film it in Vancouver. 

The Vancouver-filmed seasons average a score of 8.12, while those filmed in Los Angeles get an 8.04. Comparing this to the series mean  of 8.09 and standard deviation of 0.68, it doesn't look like a very significant result, but it has validated my feelings.  

# Footnotes

<sup> [1] </sup>

"Episodes marked with an asterisk (\*) are considered mythology/conspiracy (mytharc) shows and deal with colonisation, alien invasion, black oil, abduction scenarios etc. Non-asterisked episodes are Monster of the Week (MOTW) shows.) " http://www.insidethex.co.uk

<sup> [2] </sup>

"Chris Carter is returning to the helm, will pen the scripts and will also serve as an executive producer on The X-Files revival" http://www.tvwise.co.uk/2015/03/the-x-files-revival-nears-greenlight-at-fox-network-eyes-short-order-gillian-anderson-david-duchovny-to-return/

<sup> [3] </sup>

"When queried about the writers and producers that could join his team, Carter confirms that Glen Morgan will be coming back in a productorial position. 'We've lured Darin Morgan and Jim Wong, we're very excited about that and we're working on the rest.' He adds. Hopefully we can get a confirmation on Frank Spotnitz soon enough." https://web.archive.org/web/20160125142527/http://www.xfiles.news/index.php/news/latest-news/85-xfn-exclusive-chris-carter-on-xfilesrevival
