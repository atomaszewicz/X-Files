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

Let's get down to it, which are better the *MotW* or the *mytharc* episodes.
```
> mean(subset(xfiles$rating,xfiles$motw=="Y"))
[1] 7.8552

> mean(subset(xfiles$rating,xfiles$motw=="N"))
[1] 8.475
```


