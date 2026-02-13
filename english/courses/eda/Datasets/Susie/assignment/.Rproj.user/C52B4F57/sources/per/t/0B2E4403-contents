Fledgling <- read.csv("C:/Users/01438475/Google Drive/UCTcourses/DataScience/LectureNotes/EDA/Datasets/Susie/Data.Bourne_FledglingSurvival.csv")
Nestlings <- read.csv("C:/Users/01438475/Google Drive/UCTcourses/DataScience/LectureNotes/EDA/Datasets/Susie/Data.Bourne_NestlingsAllData.csv")

#make dates

library(tidyverse)
library(lubridate)
library(survival)
library(survminer)
library(nlme)
library(foreign)
library(lme4)

Fledgling = Fledgling %>% 
  mutate(dateNew = make_date(Year, Month, Day)) %>%
  select(dateNew, BirdID, SurvPeriod)

Nestlings = Nestlings %>% 
  mutate(dateNew = make_date(Year, Month, Day)) %>%
  rename(Group = GRP) %>%
  select(4:84)

new = left_join(Nestlings, Fledgling, by = c("dateNew", "BirdID"))
GroupCount = new %>% group_by(Group) %>% count()
means = new %>% group_by(bird) %>% 
  summarize(Massmean = mean(Mass) )
  
new = left_join(new, GroupCount, by="Group") 
new = left_join(new, means, by="bird") 

new = new %>% filter(new$n >2)

new = new %>% filter(is.na(Mass) == FALSE) 
new$GrpSizeTotal = as.numeric(new$GrpSizeTotal)

# Line Graph

p <- new %>% group_by(bird) %>%
  ggplot(mapping = aes(x = dateNew, y = Mass, group = Group))

p + geom_line()

p + geom_line(aes(group = Group, color = Group)) 

p + geom_line(aes(group = Group, color = Group)) +
  stat_summary(aes(group = 1), geom = "point", fun = mean,
             shape = 17, size = 3)

p + geom_line(aes(group = Group, color = Group)) + 
  facet_wrap(~ Group) + geom_jitter() 
  




new %>% group_by(bird) %>%
  ggplot(aes(x=factor(Group)))+
  geom_bar(stat="count", fill="steelblue")+
  theme_minimal()





# Boxplot

new %>% group_by(Group) %>% 
  ggplot() + 
  geom_boxplot(aes(x = dateNew, y= Mass, fill = Group)) +
  theme_minimal()

+ geom_jitter(width = 0.2)
+ facet_grid("Tmaxcat")
