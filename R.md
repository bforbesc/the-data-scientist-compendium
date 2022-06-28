# R

TBD
```
rm(list=ls())

colnames()

sum(duplicated(df$c1))

covid_munici_codes_cleaned <- covid_munici_codes %>% 
  mutate(obito = if_else(!is.na(data_obito), 1, 0, missing = NULL)) %>% 

```

[Dealing with empty and NAs](https://stackoverflow.com/questions/32556967/understanding-r-is-na-and-blank-cells)

## 📊 plotting
[Graphs side by side](https://stackoverflow.com/questions/1249548/side-by-side-plots-with-ggplot2)
```
facet_wrap(~ Hospital, labeller = label_wrap_gen(), nrow = 3)+
```

Graphs with 2 y-axis: [option (A)](https://www.r-graph-gallery.com/line-chart-dual-Y-axis-ggplot2.html); [Option (B)]
(https://rpubs.com/MarkusLoew/226759)


[Colors palette](https://www.nceas.ucsb.edu/sites/default/files/2020-04/colorPaletteCheatsheet.pdf)

[Dealing with duplicates](https://stats.stackexchange.com/questions/6759/removing-duplicated-rows-data-frame-in-r)
```
# check for duplicates 
nos_data_raw[duplicated(nos_data_raw),]


library(dplyr)  
df %>%   
  group_by(Date) %>%   
  summarise(uniqueid = n_distinct(ID))
```

[Changing labels](https://www.datanovia.com/en/lessons/rename-data-frame-columns-in-r/)
```
my_data %>%  
  rename( 
    sepal_length = Sepal.Length, 
    sepal_width = Sepal.Width 
    )

names(my_data)[1] <- "sepal_length"
```

Dates
```
nos_google_median <- nos_google_raw %>% 
  filter(data >= "2020-01-06" & data <= "2020-02-09") %>% 
  mutate(week_day = wday(data), week_day_name = weekdays(data, abbreviate = TRUE))  %>% 
  group_by(concelho, week_day, week_day_name)%>% 
  summarise(median_week_day = median(stay_home)) 
nos_data_delta20 <- nos_data_raw_delta20 %>% 
  filter(week_day %in% c(2, 3, 4, 5, 6))%>%
```

[Moving averages](https://www.storybench.org/how-to-calculate-a-rolling-average-in-r/)

[Dealing with accents](https://stackoverflow.com/questions/52908963/import-csv-file-with-accent-characters-in-r)

[Deal with upper and lower cases](https://www.geeksforgeeks.org/convert-first-letter-of-every-word-to-uppercase-in-r-programming-str_to_title-function/)

[Joining tables](https://rpubs.com/williamsurles/293454)
