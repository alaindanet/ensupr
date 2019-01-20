<!-- README.md is generated from README.Rmd. Please edit that file -->
Goal
====

Analyse data on superior education and research in France.

Non permanent employement in french universities
================================================

``` r
library(tidyverse)
library(magrittr)
# Data from here: https://data.enseignementsup-recherche.gouv.fr/explore/dataset/fr-esr-enseignants-nonpermanents-esr-public/
job <- readr::read_delim("https://data.enseignementsup-recherche.gouv.fr/explore/dataset/fr-esr-enseignants-nonpermanents-esr-public/download/?format=csv&timezone=Europe/Berlin&use_labels_for_header=true", delim=";")
colnames(job) %<>% str_to_lower(.)

# summary by year
job_year <- job %>%
  group_by(rentrée) %>%
  summarise(effectif = sum(effectif))

# What is happening in 2014? 
ggplot(job_year, aes(x = rentrée, y = effectif)) +
  geom_point() +
  geom_line()
```
