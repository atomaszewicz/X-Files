# Monster of the Week vs. Conspiracy Episodes

## Set-Up

As in my previous projects I use IMDb's [user ratings of episodes](http://www.imdb.com/title/tt0106179/epdate?ref_=ttep_ql_3). I've scraped it into Excel, cleaned it up and now we bring it into RStudio to analyze. We begin in RStudio by loading some packages.

```
install.packages("xlsx") 
install.packages("ggplot2")
require("xlsx")
require("ggplot2")
```
Now bring in the Excel spreadsheet

```xfiles<-read.xlsx("x_files.xlsx",1)```

To start our analysis of the two types of episodes, we must begin by discuss their distinctions. 

*Conspiracy* episodes, aka *mytharc*, are those that feature Mulder and Scully investigating the series-arcing government conspiracy about aliens, while *monster of the week* (*motw*) episodes are one-off investigations of some paranormal or otherwise mysterious 'X-File'. Most episodes fit into one of these two distinct categories but sometimes government conspiracy  elements bleed into MotW episodes, and vice-versa. After straining my personal knowledge and memory of the show I decided to work with the classifications done by the phenomenal website http://www.insidethex.co.uk (they have transcribed every episode of the show by-hand!). Their method is to classify episodes as *mytharc* only if they directly feature elements of the government conspiracy <sup> [1] </sup>. 

In Excel I created a column titled '*motw*' and classified each episode as 'Y' or 'N' to enter this information.

The only other big decision for this project is whether or not to include the 10th season revival from 2016. Though the series creator and executive producer Chris Carter back on the series along with some of the main writers and other staff <sup> [2] </sup> <sup> [3] </sup> I believe that too much time has passed, and too much has changed from the original airing for it to be compared, and decided to leave it out.

## First Look

The X-Files average and median episode score is 8.1/10, with the highest and lowest rated episodes scoring 9.4 and 6.0 respectively. There are 125 *motw* shows, which average a score of 7.8, and 76 *mytharc* episodes which average 8.5. So the *mytharc* episodes are a little above average, and the *motw* episodes a little below.

![rate_box_jitter](https://raw.githubusercontent.com/atomaszewicz/X-Files/master/RStudio/Plots/rate_box_jitter.png)

## Seaons change...

As expected we see the majority of *motw* episodes below and *mytharc* episodes above the median. How do the ratings change when one shifts from a *motw* to a *mytharc* episode, or vice-versa?


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

In summary, we have created two new columns, one which logs whether the previous and current episodes are *motw* shows, and one with the difference in score between those two. For example: episode 2 is rated 8.3 and is **not** a *motw* episode, while episode 3 is rated 8.7 and **is** a *motw* episode, so the two columns read 'N->Y' and '0.4'. From now on we will drop the arrow and simply refer to these transitions with the two letters.

The YN and NY transitions both occur 36 times, NN 39 times, and YY jump up at 89 times. Though there are 125 *motw* and 76 *mytharc*, it is still surprising how few NN occurances there are, but it shows that 50% of *mytharc* episodes sit between 2 *motw* episodes (we will come back to this later).

Unsuprsingly the difference in score between episodes of the same type are very small, with both NN and YY having medians of 0, and averages of -0.09 and -0.04 respectively. It is interesting that they are both negative, but the difffernces aren't large enough to be significant. 

The YN and NY sets align with our previously-learned facts, the *mytharc* shows are of higher quality than the *motw* ones. YN transitions (i.e. going from *motw* to *mytharc*) saw a notable up-tick, with both the median and average being positive (0.6 and 0.6 respecitvely) and likewise for the NY transfer's metrics being negative (-0.3 and -0.4 respecitvely).






