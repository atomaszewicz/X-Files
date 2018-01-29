# Monster of the Week vs. Conspiracy Episodes

## Set-Up

As in my previous projects I will use IMDb's [user ratings](http://www.imdb.com/title/tt0106179/epdate?ref_=ttep_ql_3) to quantify 'quality'. I've scraped this data into Excel, where I cleaned it up, and now we bring it into RStudio to analyze. We begin by loading some packages.

```
install.packages("xlsx") 
install.packages("ggplot2")
require("xlsx")
require("ggplot2")
```
Now we bring in the [Excel spreadsheet](https://github.com/atomaszewicz/X-Files/blob/master/Data/x0files.xlsx) into a dataframe called 'xfiles'.

```xfiles<-read.xlsx("x_files.xlsx",1)```

To start our analysis, we must begin by discussing the two types of episodes. 

*Conspiracy* episodes, aka *mytharc*, are those that feature Mulder and Scully investigating the series-arcing government conspiracy about aliens. Then we have the *monster of the week* (*motw*) episodes which are one-off investigations of paranormal or otherwise mysterious events. Most episodes fit easily into one of the two categories but sometimes elements of one bleed into the other. After straining my personal knowledge and memory of the show, I decided to work with the classifications done by the phenomenal website http://www.insidethex.co.uk (they have transcribed every episode of the show by-hand!) <sup> [1] </sup>. 

To keep track of the type I created a column titled 'motw' and classified each episode with 'Y' or 'N'.

The only other big decision for this project is whether or not to include the 10th season revival from 2016. Though the series creator and executive producer Chris Carter are back on the series, along with some of the main writers and other staff <sup> [2] </sup> <sup> [3] </sup, I believe that too much time has passed, and too much has changed for it to be a useful comparison. Thus I have decided to only use the original run of seasons 1-9 in my analysis.

## First Look

The X-Files average and median episode score is 8.1/10 with a standard deviation of 0.7, with the highest and lowest rated episodes scoring 9.4 and 6.0 respectively. There are 125 *motw* shows, which average a score of 7.8, and 76 *mytharc* episodes which average 8.5. So the *mytharc* episodes are a little above average, and the *monster* episodes a little below. As the more formulaic and predicatble of the two, and seen by some as filler, it's no great suprise that the *motw* episodes finish below average.

![rate_box_jitter](https://raw.githubusercontent.com/atomaszewicz/X-Files/master/RStudio/Plots/rate_box_jitter.png)


## Seasons change...

Not a single season has average *mytharc* shows finishing behind average *motw* shows. Though I like the alien conspiracy episodes more in general, towards the end of the series they get a little disjointed, outlandish, and confusing (yes, even for a show about monsters and aliens). This difference isn't nominal either, two thirds of the seasons see the two episode types ratings split by over 0.6 points.

All but the final season's *mytharc* ratings are above the series' average score of 8.1, and only two season's *motw* scores are above this average.

![season_avg_type](https://raw.githubusercontent.com/atomaszewicz/X-Files/master/RStudio/Plots/season_avg_type.png?raw=TRUE)


## A Little of Column A, a Little of Column B


Next we want to look at how the ratings change when one shifts between episode types. To study this we have to add some columns to our dataframe. 

```
#For each episode we check if it's motw status (Y/N) is the same or different from the last episode's
#We indicate the type of change in a new column 'chng' (there are 4 types of changess: YY, YN, NY, NN)
#Example: 'Y->N' episode i-1 was a motw, but the current episode i is not a motw episode

for(i in 2:max(xfiles$total_ep_num)){
      if(xfiles$motw[i-1]=="N"&&xfiles$motw[i]=="Y"){
          xfiles$chng[i]="N->Y"
      } else if(xfiles$motw[i-1]=="Y"&&xfiles$motw[i]=="N"){
          xfiles$chng[i]="Y->N"
      } else if (xfiles$motw[i-1]=="N"&&xfiles$motw[i]=="N"){
          xfiles$chng[i]="N->N"
      } else xfiles$chng[i]="Y->Y"
 }
#Into a new column 'chng_val' we input the value of the difference in rating between the last episode and the current one

for(i in 2:max(xfiles$total_ep_num)){
     xfiles$chng_val[i]<-(xfiles$rate[i]-xfiles$rate[i-1])
}
```

In summary, we have created two new columns, one which logs whether the previous and current episodes are *motw* shows, and one with the difference in score between those two. For example: episode 2 is rated 8.3 and is **not** a *motw* episode, while episode 3 is rated 8.7 and **is** a *motw* episode, so the two columns read 'N->Y' and '0.4'. From now on we will drop the arrow and simply refer to these transitions with the two letters (in our example 'NY').

Throughout the series the YN and NY transitions occur 36 times each, NN 39 times, and YY 89 times. Though there are 125 *motw* and 76 *mytharc*, where over 50% of *mytharc* episodes are sandwiched between two *motw* episodes.

Unsuprsingly the difference in score between episodes of the same type are very small. Both NN and YY have a median difference of 0, and average difference of -0.09 and -0.04 respectively. It is interesting that they are both negative, but since we are adding many positive and negative values it is likely not significant (I won't investiagte this to keep my promise of this being a short project). 

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

# Plots

## Rating Boxplot

``rate_box<-ggplot(xfiles,aes(x=season_num,y=rating,group=season_num))+geom_boxplot()+geom_point(aes(col=motw))+scale_x_continuous(breaks=c(1,3,5,7,9))+scale_colour_discrete(name="Episode Type",labels=c("Mytharc","Monster of\n  the Week"))+xlab("Season Number")+ylab("IMDb Rating")+ggtitle("Monsters vs. Aliens",subtitle="The X-Files")``

## Season Bar Chart
``season_avg_type<-ggplot(season_avg,aes(x=season,y=value))+geom_bar(aes(fill=variable),stat="identity",position="dodge")+coord_cartesian(ylim=c(7,9))+xlab("Season Number")+ylab("IMDb Rating")+ggtitle("Battle of the Types",subtitle="X-Files Season Averages by Episode Type")+scale_x_continuous(breaks=c(1,3,5,7,9))+scale_fill_discrete(name="Episode Type")``




