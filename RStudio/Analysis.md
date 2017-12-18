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

*Conspiracy* episodes, aka *mytharc*, are those that feature Mulder and Scully investigating the series-arcing government conspiracy about aliens, while *Monster of the Week* (*MotW*) episodes are one-off investigations of some paranormal or otherwise mysterious 'X-File'. Most episodes fit into one of these two distinct categories but sometimes government conspiracy  elements bleed into MotW episodes, and vice-versa. After straining my personal knowledge and memory of the show I decided to work with the classifications done by the phenomenal website http://www.insidethex.co.uk (they have transcribed every episode of the show by-hand!). Their method is to classify episodes as *mytharc* only if they directly feature elements of the government conspiracy <sup> [1] </sup>. 

In Excel I created a column titled '*MotW*' and classified each episode as 'Y' or 'N' to enter this information.

The only other big decision for this project is whether or not to include the 10th season revival from 2016. With the series creator and executive producer Chris Carter back on the series along with some of the main writers and other staff <sup> [2] </sup> <sup> [3] </sup>. I was tempted to include the 10th season in my analysis, but I believe that still too much time has passed, and too much has changed from the original airing for it to be compared, and decided to leave it out.

## First Look

The show's episodes have an average rating of 8.1/10, with the highest rated episode scoring a 9.4 and the lowest a 6.0. There are 125 *MotW*, which average a score of 7.8, and 76 *mytharc* episodes, . The average score of the *MotW* shows is 7.8, and the *mytharc*'s 8.5. 

So the *mytharc* episodes are 0.4 points better than average and 0.6 better than the *MotW* episodes. 

```
for(i in 2:max(xfiles$total_ep_num)){
      if(xfiles$motw[i]=="Y"&&xfiles$motw[i-1]=="N"){
          xfiles$chng[i]="Y->N"
      } else if(xfiles$motw[i]=="N"&&xfiles$motw[i-1]=="Y"){
          xfiles$chng[i]="N->Y"
      } else if (xfiles$motw[i]=="N"&&xfiles$motw[i-1]=="N"){
          xfiles$chng[i]="N->N"
      } else xfiles$chng[i]="Y->Y"
 }

for(i in 2:max(xfiles$total_ep_num)){
     xfiles$chng_val[i]<-(xfiles$rate[i]-xfiles$rate[i-1])
}
```



