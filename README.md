---
title: "Creating Marcel Method Hockey"
author: "Alex Walker"
date: "14/08/2020"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
options(knitr.table.format = 'markdown')

library(tidyverse) 
library(here) 
library(readxl) 
library(stringr) 
library(dplyr) 
library(ggplot2) 
library(knitr)
library(kableExtra)

#Loading every library known to man. 

season_1718 <- read_csv(here("data","1718_season.csv"))
season_1819 <- read_csv(here("data","1819_season.csv"))
season_1920 <- read_csv(here("data","1920_season.csv"))

#Load in our 3 season we're going to be using for the Marcel Method

names(season_1718)

#Things to note: In order to complete Marcel projections I need 1) Season weights (I'm sticking with 5/4/3) 2) I'll need to find each players average in the relevant seasons 3) I'll need to find the league average for F/D in each category 4) Regress the player usiong the league average at their position 5) Determine their projected TOI 6) Apply age adjustment 7) adjust based on 2020 baseline


#Finding the league averages for the stats we're going to use is the first order of business: 


mean_1920 <- season_1920 %>%
          mutate(Pos = replace(Pos, Pos != "D", "F")) %>%
          group_by(Pos) %>%
          summarize(
          avg_G = mean(G, na.rm = TRUE),
          avg_A = mean(A, na.rm = TRUE),
          avg_PTS = mean(PTS, na.rm = TRUE),
          avg_PPG = mean(PPG, na.rm = TRUE),
          avg_PPA = mean(PPA, na.rm = TRUE),
          avg_S = mean(S, na.rm = TRUE),
          avg_BLK = mean(BLK, na.rm = TRUE),
          avg_HIT = mean(HIT, na.rm = TRUE),
          avg_PIM = mean(PIM, na.rm = TRUE),
          avg_FOW = mean(FOW, na.rm = TRUE),
          avg_FOL = mean(FOL, na.rm = TRUE),
          avg_TOI = mean(TOI, na.rm = TRUE),
          n = n())

      
table_1920 <- mean_1920 %>%
    kable() %>%
    kable_styling()
        

