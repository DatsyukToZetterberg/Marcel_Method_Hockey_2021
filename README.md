---
title: "Creating Marcel Method Hockey"
author: "Alex Walker"
date: "14/08/2020"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

library(tidyverse) 
library(here) 
library(readxl) 
library(stringr) 
library(dplyr) 
library(ggplot2) 
library(knitr)

#Loading every library known to man. 

season_1718 <- read_csv(here("data","1718_season.csv"))
season_1819 <- read_csv(here("data","1819_season.csv"))
season_1920 <- read_csv(here("data","1920_season.csv"))

#Load in our 3 season we're going to be using for the Marcel Method

names(season_1718)

#Things to note: In order to complete Marcel projections I need 1) Season weights (I'm sticking with 5/4/3) 2) I'll need to find each players average in the relevant seasons 3) I'll need to find the league average for F/D in each category 4) Regress the player usiong the league average at their position 5) Determine their projected TOI 6) Apply age adjustment 7) adjust based on 2020 baseline

filtered_1718 <- season_1718 %>%
              select(Player, Age, Tm, Pos, GP, G, A, PTS, PPG, PPA, S, BLK, HIT, PIM, FOW, FOL, TOI)
           
filtered_1819 <- season_1819 %>%
              select(Player, Age, Tm, Pos, GP, G, A, PTS, PPG, PPA, S, BLK, HIT, PIM, FOW, FOL, TOI)

filtered_1920 <- season_1920 %>%
              select(Player, Age, Tm, Pos, GP, G, A, PTS, PPG, PPA, S, BLK, HIT, PIM, FOW, FOL, TOI)

filtered_1920 %>%
  group_by(Pos) %>%
  sum(filtered_1920,
            mean_G = mean(G))

        
        