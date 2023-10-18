# dogs_about_town
## Tracking the dogs I see in Lubbock, TX
library(dplyr)
library(ggplot2)
library(tidyr)
library(ggthemes)

date <- seq(from = as.Date("2023-09-13"), to = as.Date("2023-10-13"), by = 'day')

saw <- c(2,0,0,0,0,6,0,2,0,0,0,0,3,0,1,0,0,0,0,0,0,1,1,0,0,0,2,4,1,0,0)
  
chased <- c(0,2,0,0,0,0,1,1,1,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,0,1,0,2,0,0)

non_bike <- c(0,0,1,1,1,0,0,0,0,1,1,1,0,0,0,0,1,1,1,0,1,0,0,0,1,1,0,0,0,0,1)

d <- data.frame(date,saw,chased,non_bike) %>% 
  pivot_longer(!date, names_to = "dogs", values_to = "count")

ggplot(d, aes(fill=dogs, y=count, x=date)) + 
  geom_bar(position="stack", stat="identity") + theme_tufte() +
  xlab("Date") + ylab("Number of Loose Dogs Seen") +
  theme(legend.title= element_blank())+
  scale_fill_manual(breaks = c("saw", "chased", "non_bike"),
                      labels=c('Dogs That Chased Me','Dogs I Saw','Days I Didn\'t Bike'),
                      values = c("#56B4E9","#D55E00","#999999"))

sum(saw)/18 #1.28

sum(chased)/18 #.5

sum(chased)/sum(saw) #39% of dogs I see chase me


