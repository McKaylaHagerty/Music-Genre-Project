
Homework 8

McKayla Hagerty

CS 625, Fall 2020

## Preparing Data

Original Source:
<https://data.world/kcmillersean/billboard-hot-100-1958-2017> (the
orginial dataset was scraped using import.io)

Original Source:
<https://data.world/kcmillersean/billboard-hot-100-1958-2017> (the
original dataset was pulled from Spotify Web API)

``` r
#Import Billboard data.
billboard <- read.csv("https://query.data.world/s/j53mutis3fjnygz4fjctj576eljh32", header=TRUE, stringsAsFactors=FALSE)
billboard$WeekID <- as.Date(billboard$WeekID , format = "%m/%d/%Y")
View(billboard)
```

``` r
library("httr") 
library("readxl")
GET("https://query.data.world/s/5phlvfg3im7qyffzy66v4m2uvzmnr3", write_disk(tf <- tempfile(fileext = ".xlsx")))
```

    ## Response [https://download.data.world/file_download/kcmillersean/billboard-hot-100-1958-2017/Hot%20100%20Audio%20Features.xlsx?auth=eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJwcm9kLXVzZXItY2xpZW50Om1ja2F5bGFoYWdlcnR5IiwiaXNzIjoiYWdlbnQ6bWNrYXlsYWhhZ2VydHk6OmE0ZGU1MTNlLTY5Y2UtNDY4YS05ZTc2LTRkMzFlMzAxZDI0ZiIsImlhdCI6MTYwNjM0MDk2OCwicm9sZSI6WyJ1c2VyIiwidXNlcl9hcGlfYWRtaW4iLCJ1c2VyX2FwaV9yZWFkIiwidXNlcl9hcGlfd3JpdGUiXSwiZ2VuZXJhbC1wdXJwb3NlIjpmYWxzZSwidXJsIjoiNTgzMTYzZTAyMTU0OTNjMTI3NzE4OTg1ZTkyMzk1YjY0MzEzYTc0NyJ9.snQDN2aVskJ-HU8NRNFwtZliVYi7bpnG2Hkr9NjQLcxvVEyjARmhiRhDAn6Xc3p3-4_mOQBh_sINHHyfzSegyQ]
    ##   Date: 2020-12-11 15:38
    ##   Status: 200
    ##   Content-Type: application/vnd.openxmlformats-officedocument.spreadsheetml.sheet
    ##   Size: 5.73 MB
    ## <ON DISK>  C:\Users\13mck\AppData\Local\Temp\Rtmp06O30W\file2b286ecb520.xlsx

``` r
genres_first_look <- read_excel(tf)
names(genres_first_look)
```

    ##  [1] "SongID"                    "Performer"                
    ##  [3] "Song"                      "spotify_genre"            
    ##  [5] "spotify_track_id"          "spotify_track_preview_url"
    ##  [7] "spotify_track_album"       "spotify_track_explicit"   
    ##  [9] "spotify_track_duration_ms" "spotify_track_popularity" 
    ## [11] "danceability"              "energy"                   
    ## [13] "key"                       "loudness"                 
    ## [15] "mode"                      "speechiness"              
    ## [17] "acousticness"              "instrumentalness"         
    ## [19] "liveness"                  "valence"                  
    ## [21] "tempo"                     "time_signature"

``` r
#Cleaned genre data.
genres <- read.csv("C:/Users/13mck/Desktop/genres-final.csv")
names(genres)
```

    ##  [1] "SongID"                    "Performer"                
    ##  [3] "Song"                      "spotify_genre.1"          
    ##  [5] "Genre"                     "spotify_track_id"         
    ##  [7] "spotify_track_preview_url" "spotify_track_album"      
    ##  [9] "spotify_track_explicit"    "spotify_track_duration_ms"
    ## [11] "spotify_track_popularity"  "danceability"             
    ## [13] "energy"                    "key"                      
    ## [15] "loudness"                  "mode"                     
    ## [17] "speechiness"               "acousticness"             
    ## [19] "instrumentalness"          "liveness"                 
    ## [21] "valence"                   "tempo"                    
    ## [23] "time_signature"

``` r
head(genres)
```

    ##                                               SongID
    ## 1                      AdictoTainy, Anuel AA & Ozuna
    ## 2 The Ones That Didn't Make It Back HomeJustin Moore
    ## 3                  ShallowLady Gaga & Bradley Cooper
    ## 4                EnemiesPost Malone Featuring DaBaby
    ## 5    Bacc At It AgainYella Beezy, Gucci Mane & Quavo
    ## 6                             The ArcherTaylor Swift
    ##                         Performer                                   Song
    ## 1         Tainy, Anuel AA & Ozuna                                 Adicto
    ## 2                    Justin Moore The Ones That Didn't Make It Back Home
    ## 3      Lady Gaga & Bradley Cooper                                Shallow
    ## 4    Post Malone Featuring DaBaby                                Enemies
    ## 5 Yella Beezy, Gucci Mane & Quavo                       Bacc At It Again
    ## 6                    Taylor Swift                             The Archer
    ##    spotify_genre.1       Genre       spotify_track_id
    ## 1    pop reggaeton         pop 3jbT1Y5MoPwEIpZndDDwVq
    ## 2 arkansas country     country                       
    ## 3        dance pop         pop 2VxeLyX666F8uXCJ0dZF8B
    ## 4          dfw rap hip-hop/rnb 0Xek5rqai2jcOWCYWJfVCF
    ## 5          dfw rap hip-hop/rnb 2biNa12dMbHJrHVFRt8JyO
    ## 6        dance pop         pop 3pHkh7d0lzM2AldUtz2x37
    ##                                                                                     spotify_track_preview_url
    ## 1                                                                                                            
    ## 2                                                                                                            
    ## 3                                                                                                            
    ## 4                                                                                                            
    ## 5 https://p.scdn.co/mp3-preview/fa6fa6f6f363be29ae45af3470675ef5cbcd081f?cid=b8d3901151d34489a160e3cf0ab1fa94
    ## 6                                                                                                            
    ##              spotify_track_album spotify_track_explicit
    ## 1 Adicto (with Anuel AA & Ozuna)                  FALSE
    ## 2                                                    NA
    ## 3      A Star Is Born Soundtrack                  FALSE
    ## 4           Hollywood's Bleeding                   TRUE
    ## 5               Bacc At It Again                   TRUE
    ## 6                          Lover                  FALSE
    ##   spotify_track_duration_ms spotify_track_popularity danceability energy key
    ## 1                    270740                       91        0.734  0.836  10
    ## 2                        NA                       NA           NA     NA  NA
    ## 3                    215733                       88        0.572  0.385   7
    ## 4                    196760                       86        0.542  0.674   6
    ## 5                    228185                       61        0.948  0.623   8
    ## 6                    211240                       76        0.292  0.574   0
    ##   loudness mode speechiness acousticness instrumentalness liveness valence
    ## 1   -4.803    0      0.0735      0.01700         1.64e-05   0.1790   0.623
    ## 2       NA   NA          NA           NA               NA       NA      NA
    ## 3   -6.362    1      0.0308      0.37100         0.00e+00   0.2310   0.323
    ## 4   -4.169    1      0.2100      0.05880         0.00e+00   0.0955   0.667
    ## 5   -5.725    0      0.1680      0.00124         1.07e-06   0.0716   0.856
    ## 6   -9.375    1      0.0401      0.12000         5.69e-03   0.0663   0.166
    ##     tempo time_signature
    ## 1  80.002              4
    ## 2      NA             NA
    ## 3  95.799              4
    ## 4  76.388              4
    ## 5 135.979              4
    ## 6 124.344              4

``` r
#Removing duplicate SongID rows in the genre dataset to allow for merging. 
genres <- genres[!duplicated(genres[c('SongID')]),] 
```

``` r
merged<-merge(billboard, genres, by = "SongID",all.x=TRUE)
merged$WeekID <- as.Date(merged$WeekID , format = "%m/%d/%Y")

View(merged) 
```

``` r
#Creating new column for year, month, and day. 
library(tidyr)
```

    ## 
    ## Attaching package: 'tidyr'

    ## The following object is masked _by_ '.GlobalEnv':
    ## 
    ##     billboard

``` r
merged <- merged %>%
  separate(WeekID, sep="-", into = c("year", "month", "day"))
```

``` r
#New dataframe for mean for each year.
library(dplyr)
```

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
mean_data <- group_by(merged, year) %>%
             summarise(danceability = mean(danceability, na.rm = TRUE),energy = mean(energy, na.rm = TRUE),speechiness = mean(speechiness, na.rm = TRUE),acousticness = mean(acousticness, na.rm = TRUE),liveness = mean(liveness, na.rm = TRUE),valence = mean(valence, na.rm = TRUE),loudness = mean(loudness, na.rm = TRUE))
```

    ## `summarise()` ungrouping output (override with `.groups` argument)

``` r
mean_data <- as.data.frame(mean_data)

class(mean_data)
```

    ## [1] "data.frame"

``` r
library(ggplot2)
ggplot(data = mean_data, aes(x = year,group = 1)) + 
  geom_line(aes(y = danceability),color="blue") + 
  geom_line(aes(y = energy),color="green") +
  geom_line(aes(y = speechiness),color="purple") +
  geom_line(aes(y = acousticness),color="red") +
  geom_line(aes(y = liveness),color="orange") +
  geom_line(aes(y = valence)) +
  labs(y = "") # Delete or change y axis title if desired.
```

![](report_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

This is interesting. I can see how traits of what makes a top 100 song
have changed over the years. This can especially be seen in the
acousticness and valence. From previous findings, we would expect
something interesting from the loudness as well.

I also remember reading about radar charts and wonder if I could make an
interactive radar chart with a slider to look into the traits for each
year or decade. Or perhaps I could make one with an overlapping view
with averages by decade. The problem with radar charts is that it is
difficult to compare or get a sense of a specific measurement. However,
if I layered them then comparing would be easier. Also, exact values are
not the point of showing this data. The value is in the comparison
between years or decades.

The last trait I haven’t spent much time on is the genre. I would like
to see the change over time in what genres make the top 100 list. I’ll
first start with a stacked bar chart as use the years column rather than
the WeekID column. *Has the popularity of different genres changed over
time?*

``` r
genrebyyear <- table(merged$year, merged$Genre) 
genrebyyear <- as.data.frame(genrebyyear)
names(genrebyyear)[names(genrebyyear) == "Var1"] <- "year"
names(genrebyyear)[names(genrebyyear) == "Var2"] <- "Genre"
names(genrebyyear)[names(genrebyyear) == "Freq"] <- "Count"
```

``` r
# library
library(ggplot2)
topgenrebyyear <- genrebyyear %>% filter(Genre %in% c("rock", "pop","alternative/indie","electronic/dance","soul","hip-hop/rnb","country"))
  

# Stacked
ggplot(topgenrebyyear, aes(fill=Genre, y=Count, x=year)) + 
    geom_bar(position="stack", stat="identity")
```

![](report_files/figure-gfm/unnamed-chunk-10-1.png)<!-- -->

I don’t generally like stacked bar graphs because it is difficult to
make comparisons between groups. However, I discovered streamgraphs
which may be a better fit.

“Streamgraphs are a generalization of stacked area graphs where the
baseline is free. By shifting the baseline, it is possible to minimize
the change in slope (or wiggle) in individual series, thereby making it
easier to perceive the thickness of any given layer across the data.
Byron & Wattenberg describe several streamgraph algorithms in ‘Stacked
Graphs—Geometry & Aesthetics3’”4

``` r
#installing and loading streamgraph
#install.packages("devtools")
library(devtools)
```

    ## Loading required package: usethis

``` r
#install.packages("zoo")
devtools::install_github("hrbrmstr/streamgraph")
```

    ## WARNING: Rtools is required to build R packages, but is not currently installed.
    ## 
    ## Please download and install Rtools 4.0 from https://cran.r-project.org/bin/windows/Rtools/.

    ## Skipping install of 'streamgraph' from a github remote, the SHA1 (76f7173e) has not changed since last install.
    ##   Use `force = TRUE` to force installation

``` r
topgenrebyyear$year <- as.Date(topgenrebyyear$year, format="%Y")
```

``` r
library(dplyr)
library(streamgraph)

#topgenrebyyear %>% 
  #streamgraph(key="Genre", value="Count", date="year", interpolate="linear", sort=TRUE)%>%     #sg_fill_brewer("PuOr")%>%
  #sg_fill_manual(c("black", "#ffa500", "blue", "white", "#00ff00", "red")) %>% 
  #sg_axis_x(tick_interval=3, tick_units="year","%Y") 
  #sg_legend(FALSE, "Genre: ")
```

Should I choose to move forward with this chart, I would like to add key
genre labels and more appropriate colors. The axis labels would also
need adjusted. As mentioned before, if I continue down this route for my
final visualization, I will probably return to the cleaning to see if I
can show more of a representation of the pre-1990 song genres.

At this point, Professor Weigle suggested I consider also looking into
how particular genres have changed over time. To see if there was
something interesting to be discovered there, I will create three new
datasets with just rock, pop, and country music and create a multiple
line plot for each featuring the music characteristics as before. *How
have popular songs in key genres changed over time?*

``` r
library(ggplot2)
rockmusic <- merged %>% filter(Genre %in% c("rock"))
```

``` r
#New dataframe for mean for each year for just rock music.
library(dplyr)
mean_data_rockmusic <- group_by(rockmusic, year) %>%
             summarise(danceability = mean(danceability, na.rm = TRUE),energy = mean(energy, na.rm = TRUE),speechiness = mean(speechiness, na.rm = TRUE),acousticness = mean(acousticness, na.rm = TRUE),liveness = mean(liveness, na.rm = TRUE),valence = mean(valence, na.rm = TRUE),loudness = mean(loudness, na.rm = TRUE))
```

    ## `summarise()` ungrouping output (override with `.groups` argument)

``` r
mean_data_rockmusic <- as.data.frame(mean_data_rockmusic)

class(mean_data_rockmusic)
```

    ## [1] "data.frame"

``` r
p1 <- ggplot(data = mean_data_rockmusic, aes(x = year,group = 1)) + 
  geom_line(aes(y = danceability),color="blue") + 
  geom_line(aes(y = energy),color="green") +
  geom_line(aes(y = speechiness),color="purple") +
  geom_line(aes(y = acousticness),color="red") +
  geom_line(aes(y = liveness),color="orange") +
  geom_line(aes(y = valence)) +
  labs(y = "") # Delete or change y axis title if desired.
p1+theme(axis.text.x = element_text(angle = 90,vjust = .5))
```

![](report_files/figure-gfm/unnamed-chunk-15-1.png)<!-- -->

This is interesting. I can see how rock music has changed since 1958.

``` r
library(ggplot2)
popmusic <- merged %>% filter(Genre %in% c("pop"))
```

``` r
#New dataframe for mean for each year for just pop music.
library(dplyr)
mean_data_popmusic <- group_by(popmusic, year) %>%
             summarise(danceability = mean(danceability, na.rm = TRUE),energy = mean(energy, na.rm = TRUE),speechiness = mean(speechiness, na.rm = TRUE),acousticness = mean(acousticness, na.rm = TRUE),liveness = mean(liveness, na.rm = TRUE),valence = mean(valence, na.rm = TRUE),loudness = mean(loudness, na.rm = TRUE))
```

    ## `summarise()` ungrouping output (override with `.groups` argument)

``` r
mean_data_popmusic <- as.data.frame(mean_data_popmusic)

class(mean_data_popmusic)
```

    ## [1] "data.frame"

``` r
p1 <- ggplot(data = mean_data_popmusic, aes(x = year,group = 1)) + 
  geom_line(aes(y = danceability),color="blue") + 
  geom_line(aes(y = energy),color="green") +
  geom_line(aes(y = speechiness),color="purple") +
  geom_line(aes(y = acousticness),color="red") +
  geom_line(aes(y = liveness),color="orange") +
  geom_line(aes(y = valence)) +
  labs(y = "") # Delete or change y axis title if desired.
p1+theme(axis.text.x = element_text(angle = 90,vjust = .5))
```

![](report_files/figure-gfm/unnamed-chunk-18-1.png)<!-- -->

``` r
library(ggplot2)
countrymusic <- merged %>% filter(Genre %in% c("country"))
```

``` r
#New dataframe for mean for each year for just country music.
library(dplyr)
mean_data_countrymusic <- group_by(countrymusic, year) %>%
             summarise(danceability = mean(danceability, na.rm = TRUE),energy = mean(energy, na.rm = TRUE),speechiness = mean(speechiness, na.rm = TRUE),acousticness = mean(acousticness, na.rm = TRUE),liveness = mean(liveness, na.rm = TRUE),valence = mean(valence, na.rm = TRUE),loudness = mean(loudness, na.rm = TRUE))
```

    ## `summarise()` ungrouping output (override with `.groups` argument)

``` r
mean_data_countrymusic <- as.data.frame(mean_data_countrymusic)

class(mean_data_countrymusic)
```

    ## [1] "data.frame"

``` r
p1 <- ggplot(data = mean_data_countrymusic, aes(x = year,group = 1)) + 
  geom_line(aes(y = danceability),color="blue") + 
  geom_line(aes(y = energy),color="green") +
  geom_line(aes(y = speechiness),color="purple") +
  geom_line(aes(y = acousticness),color="red") +
  geom_line(aes(y = liveness),color="orange") +
  geom_line(aes(y = valence)) +
  labs(y = "") # Delete or change y axis title if desired.
p1+theme(axis.text.x = element_text(angle = 90,vjust = .5))
```

![](report_files/figure-gfm/unnamed-chunk-21-1.png)<!-- -->

There is certainly much to work with here. There are interesting changes
in all three genres.

## Final Questions: Results of the EDA

Question 1: *How has the prevalence of genres on the top 100 songs
billboard changed over time?*

Sketch:

``` r
#topgenrebyyear %>% 
  #streamgraph(key="Genre", value="Count", date="year", interpolate="linear", sort=TRUE)%>%     #sg_fill_brewer("PuOr")%>%
  #sg_fill_manual(c("black", "#ffa500", "blue", "white", "#00ff00", "red")) %>% 
  #sg_axis_x(tick_interval=3, tick_units="year","%Y") 
  #sg_legend(FALSE, "Genre: ")
```

The streamplot shows the main genre makeup of the top 100 songs from
1959 through 2019. It is easy to see how rock has steadily become less
popular since 1986 as pop and hip hop have taken larger percentage of
the billboard. I can also be seen that the soul genre has become less
recognized since its surge of popularity in 1965 to 1980. Country,
however, has become more popular in the 2000s.

Question 2: *How has the pop, rock, and country genres changed over
time? *

Sketches: (I will most likely choose this question for my final
visualization.)

``` r
p1 <- ggplot(data = mean_data_rockmusic, aes(x = year,group = 1)) + 
  geom_line(aes(y = danceability),color="blue") + 
  geom_line(aes(y = energy),color="green") +
  geom_line(aes(y = speechiness),color="purple") +
  geom_line(aes(y = acousticness),color="red") +
  geom_line(aes(y = liveness),color="orange") +
  geom_line(aes(y = valence)) +
  labs(y = "") # Delete or change y axis title if desired.
p1+theme(axis.text.x = element_text(angle = 90,vjust = .5))
```

![](report_files/figure-gfm/unnamed-chunk-23-1.png)<!-- -->

``` r
p1 <- ggplot(data = mean_data_popmusic, aes(x = year,group = 1)) + 
  geom_line(aes(y = danceability),color="blue") + 
  geom_line(aes(y = energy),color="green") +
  geom_line(aes(y = speechiness),color="purple") +
  geom_line(aes(y = acousticness),color="red") +
  geom_line(aes(y = liveness),color="orange") +
  geom_line(aes(y = valence)) +
  labs(y = "") # Delete or change y axis title if desired.
p1+theme(axis.text.x = element_text(angle = 90,vjust = .5))
```

![](report_files/figure-gfm/unnamed-chunk-24-1.png)<!-- -->

``` r
p1 <- ggplot(data = mean_data_countrymusic, aes(x = year,group = 1)) + 
  geom_line(aes(y = danceability),color="blue") + 
  geom_line(aes(y = energy),color="green") +
  geom_line(aes(y = speechiness),color="purple") +
  geom_line(aes(y = acousticness),color="red") +
  geom_line(aes(y = liveness),color="orange") +
  geom_line(aes(y = valence)) +
  labs(y = "") # Delete or change y axis title if desired.
p1+theme(axis.text.x = element_text(angle = 90,vjust = .5))
```

![](report_files/figure-gfm/unnamed-chunk-25-1.png)<!-- -->

## Final Visualization

``` r
library(ggplot2)
rockmusic <- merged %>% filter(merged$Genre %in% c("rock"))
```

``` r
#New dataframe for mean for each year for just rock music.
library(dplyr)
rockmusic$Decade <- 10*as.integer(as.numeric(substring(as.character(rockmusic$year), 1,4)) / 10)
mean_data_rockmusic <- group_by(rockmusic, Decade) %>%
             summarise(danceability = mean(danceability, na.rm = TRUE),energy = mean(energy, na.rm = TRUE),speechiness = mean(speechiness, na.rm = TRUE),acousticness = mean(acousticness, na.rm = TRUE),liveness = mean(liveness, na.rm = TRUE),valence = mean(valence, na.rm = TRUE),loudness = mean(loudness, na.rm = TRUE))
```

    ## `summarise()` ungrouping output (override with `.groups` argument)

``` r
mean_data_rockmusic <- as.data.frame(mean_data_rockmusic)

class(mean_data_rockmusic)
```

    ## [1] "data.frame"

``` r
library(ggplot2)
popmusic <- merged %>% filter(merged$Genre %in% c("pop"))
```

``` r
#New dataframe for mean for each year for just pop music.
library(dplyr)
popmusic$Decade <- 10*as.integer(as.numeric(substring(as.character(popmusic$year), 1,4)) / 10)
mean_data_popmusic <- group_by(popmusic, Decade) %>%
             summarise(danceability = mean(danceability, na.rm = TRUE),energy = mean(energy, na.rm = TRUE),speechiness = mean(speechiness, na.rm = TRUE),acousticness = mean(acousticness, na.rm = TRUE),liveness = mean(liveness, na.rm = TRUE),valence = mean(valence, na.rm = TRUE),loudness = mean(loudness, na.rm = TRUE))
```

    ## `summarise()` ungrouping output (override with `.groups` argument)

``` r
mean_data_popmusic <- as.data.frame(mean_data_popmusic)

class(mean_data_popmusic)
```

    ## [1] "data.frame"

``` r
library(ggplot2)
countrymusic <- merged %>% filter(merged$Genre %in% c("country"))
```

``` r
#New dataframe for mean for each year for just country music.
library(dplyr)
countrymusic$Decade <- 10*as.integer(as.numeric(substring(as.character(countrymusic$year), 1,4)) / 10)
mean_data_countrymusic <- group_by(countrymusic, Decade) %>%
             summarise(danceability = mean(danceability, na.rm = TRUE),energy = mean(energy, na.rm = TRUE),speechiness = mean(speechiness, na.rm = TRUE),acousticness = mean(acousticness, na.rm = TRUE),liveness = mean(liveness, na.rm = TRUE),valence = mean(valence, na.rm = TRUE),loudness = mean(loudness, na.rm = TRUE))
```

    ## `summarise()` ungrouping output (override with `.groups` argument)

``` r
mean_data_countrymusic <- as.data.frame(mean_data_countrymusic)

class(mean_data_countrymusic)
```

    ## [1] "data.frame"

``` r
library(ggplot2)
    
hiphoprnbmusic <- merged %>% filter(merged$Genre %in% c("   
hip-hop/rnb"))
```

``` r
#New dataframe for mean for each year for just hiphop music.
library(dplyr)
hiphoprnbmusic$Decade <- 10*as.integer(as.numeric(substring(as.character(hiphoprnbmusic$year), 1,4)) / 10)
mean_data_hiphoprnbmusic <- group_by(countrymusic, Decade) %>%
             summarise(danceability = mean(danceability, na.rm = TRUE),energy = mean(energy, na.rm = TRUE),speechiness = mean(speechiness, na.rm = TRUE),acousticness = mean(acousticness, na.rm = TRUE),liveness = mean(liveness, na.rm = TRUE),valence = mean(valence, na.rm = TRUE),loudness = mean(loudness, na.rm = TRUE))
```

    ## `summarise()` ungrouping output (override with `.groups` argument)

``` r
mean_data_hiphoprnbmusic <- as.data.frame(mean_data_hiphoprnbmusic)

class(mean_data_hiphoprnbmusic)
```

    ## [1] "data.frame"

``` r
library(dplyr)
library(ggplot2)
library(scales)
library(grid)
library(cowplot)
library(gridExtra)
```

    ## 
    ## Attaching package: 'gridExtra'

    ## The following object is masked from 'package:dplyr':
    ## 
    ##     combine

``` r
g1 <- ggplot(data = mean_data_countrymusic, aes(x = Decade,group = 1)) + 
  geom_line(size = 1.2,aes(y = danceability),color="light grey") + 
  geom_line(size = 1.2,aes(y = valence), color="dark grey")+
  geom_line(size = 2,aes(y = energy),color="mediumturquoise") +
  geom_line(size = 2,aes(y = acousticness),color="tomato2") +
  theme_bw() + 
  ylim(0, .9)+
  theme(legend.position = "none", axis.ticks = element_blank(), panel.border = element_blank(), panel.grid.major.x = element_blank(), panel.grid.minor.x = element_blank(), 
    axis.title.x = element_blank(),axis.text.y = element_blank(), axis.title.y = element_blank(), 
    axis.text.x = element_text( margin = margin(t = -8), size = 10),  
    plot.subtitle = element_text(face='bold.italic',size=10, margin = margin(b=0))) +
  annotate("text", x=2005, y=.63, label= "danceability",color="light grey", fontface =1,size = 3.5) +
  annotate("text", x=2005, y=.78, label= "energy",color="mediumturquoise", fontface =1,size = 3.5) +
  annotate("text", x=2005, y=.15, label= "acousticness",color="tomato2", fontface =1,size = 3.5) +
  annotate("text", x=2005, y=.47, label= "valence",color="dark grey", fontface =1,size = 3.5) +
  labs(subtitle = 'Qualities of Top Country Songs') 

g2 <- ggplot(data = mean_data_rockmusic, aes(x = Decade,group = 1)) + 
  geom_line(size = 1.2,aes(y = danceability),color="light grey") + 
  geom_line(size = 1.2,aes(y = valence), color="dark grey")+
  geom_line(size = 2,aes(y = energy),color="mediumturquoise") +
  geom_line(size = 2,aes(y = acousticness),color="tomato2") +
  theme_bw() + 
  ylim(0, .9)+
  theme(legend.position = "none", axis.ticks = element_blank(), panel.border = element_blank(), panel.grid.major.x = element_blank(), panel.grid.minor.x = element_blank(), 
    axis.title.x = element_blank(),axis.text.y = element_blank(), axis.title.y = element_blank(), 
    axis.text.x = element_text( margin = margin(t = -8), size = 10),  
    plot.subtitle = element_text(face='bold.italic',size=10, margin = margin(b=0))) +
  annotate("text", x=2005, y=.6, label= "danceability",color="light grey",fontface =1,size = 3.5) +
  annotate("text", x=2005, y=.83, label= "energy", color="mediumturquoise", fontface =1,size = 3.5) +
  annotate("text", x=2005, y=.14, label= "acousticness",color="tomato2",fontface =1,size = 3.5) +
  annotate("text", x=2005, y=.45, label= "valence",color="dark grey",fontface =1,size = 3.5) +
  labs( subtitle = 'Qualities of Top Rock Songs') 

g3 <- ggplot(data = mean_data_popmusic, aes(x = Decade,group = 1)) + 
  geom_line(size = 1.2,aes(y = danceability),color="light grey") + 
  geom_line(size = 1.2,aes(y = valence), color="dark grey")+
  geom_line(size = 2,aes(y = energy),color="mediumturquoise") +
  geom_line(size = 2,aes(y = acousticness),color="tomato2") +
  theme_bw() + 
  ylim(0, .9)+
  theme(legend.position = "none", axis.ticks = element_blank(), panel.border = element_blank(), panel.grid.major.x = element_blank(), panel.grid.minor.x = element_blank(), 
    axis.title.x = element_blank(),axis.text.y = element_blank(), axis.title.y = element_blank(), 
    axis.text.x = element_text( margin = margin(t = -8), size = 10),  
    plot.subtitle = element_text(face='bold.italic',size=10, margin = margin(b=0))) +
  annotate("text", x=2005, y=.625, label= "danceability",color="light grey",fontface =1,size = 3.5) +
  annotate("text", x=2005, y=.75, label= "energy",color="mediumturquoise",fontface =1,size = 3.5) +
  annotate("text", x=2005, y=.22, label= "acousticness",color="tomato2",fontface =1,size = 3.5) +
  annotate("text", x=2005, y=.51, label= "valence",color="dark grey",fontface =1,size = 3.5) +
  labs( subtitle = 'Qualities of Top Pop Songs') 

g4 <- ggplot(data = mean_data_hiphoprnbmusic, aes(x = Decade,group = 1)) + 
  geom_line(size = 1.2,aes(y = danceability),color="light grey") + 
  geom_line(size = 1.2,aes(y = valence), color="dark grey")+
  geom_line(size = 2,aes(y = energy),color="mediumturquoise") +
  geom_line(size = 2,aes(y = acousticness),color="tomato2") +
  theme_bw() + 
  ylim(0, .9)+
  theme(legend.position = "none", axis.ticks = element_blank(), panel.border = element_blank(), panel.grid.major.x = element_blank(), panel.grid.minor.x = element_blank(), 
    axis.title.x = element_blank(),axis.text.y = element_blank(), axis.title.y = element_blank(), 
    axis.text.x = element_text( margin = margin(t = -8), size = 10),  
    plot.subtitle = element_text(face='bold.italic',size=10, margin = margin(b=0))) +
  annotate("text", x=2005, y=.63, label= "danceability",color="light grey",fontface =1,size = 3.5) +
  annotate("text", x=2005, y=.78, label= "energy",color="mediumturquoise",fontface =1,size = 3.5) +
  annotate("text", x=2005, y=.15, label= "acousticness",color="tomato2",fontface =1,size = 3.5) +
  annotate("text", x=2005, y=.48, label= "valence",color="dark grey",fontface =1,size = 3.5) +
  labs( subtitle = 'Qualities of Top Hip-Hop/R&B Songs') 

grid.arrange(g1, g2, g3, g4, ncol=2,
     top = textGrob("Want to write a hit song? Maybe it's time to leave the acoustic guitar behind",x = 0, hjust = 0,gp=gpar(fontfamily="sans", fontsize=13.7,font=2,lineweight=1)))
```

![](report_files/figure-gfm/unnamed-chunk-34-1.png)<!-- -->

## Explaination

## References:

<https://stackoverflow.com/questions/40663586/streamgraph-package-in-r-will-run-the-data-but-no-graph-will-be-shown>
<https://www.quora.com/How-do-I-get-a-frequency-count-based-on-two-columns-variables-in-an-R-dataframe>
<https://stackoverflow.com/questions/10758961/how-to-convert-a-table-to-a-data-frame>
<https://www.datanovia.com/en/lessons/rename-data-frame-columns-in-r/>
<https://www.datanovia.com/en/lessons/subset-data-frame-rows-in-r/>
<https://rdrr.io/github/hrbrmstr/streamgraph/man/sg_axis_x.html>
<https://www.r-graph-gallery.com/158-change-color-in-interactive-streamgraph.html>
<https://stackoverflow.com/questions/3171426/compare-two-data-frames-to-find-the-rows-in-data-frame-1-that-are-not-present-in>
<https://community.rstudio.com/t/converting-dates-year-month-day-to-3-separate-columns-year-month-day/8585/3>
<https://stackoverflow.com/questions/35920408/creating-a-line-chart-in-r-for-the-average-value-of-groups>
<https://stackoverflow.com/questions/30375600/how-to-plot-multiple-lines-for-each-column-of-a-data-matrix-against-one-column>
<https://stackoverflow.com/questions/27082601/ggplot2-line-chart-gives-geom-path-each-group-consist-of-only-one-observation>
<https://stackoverflow.com/questions/15215457/standardize-data-columns-in-r>
<https://www.earthdatascience.org/courses/earth-analytics/time-series-data/summarize-time-series-by-month-in-r/>
