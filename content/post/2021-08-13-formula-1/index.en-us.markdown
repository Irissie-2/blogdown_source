---
title: Formula 1
author: R package build
date: '2021-08-13'
slug: index.en-us
categories: []
tags: ["Formula 1"]
keywords:
  - tech
---


# Formula 1
## Data analysis

The goal is to analyse the pit stops 
1. Which team has the fastest pit stops?
2. Which driver has the fastest pit stops?
2. Does the track make a difference in the speed of the pit stops?



Pit stop data from 1950 - 2021

```
##   raceId driverId stop lap     time duration milliseconds
## 1    841      153    1   1 17:05:23   26.898        26898
## 2    841       30    1   1 17:05:52   25.021        25021
## 3    841       17    1  11 17:20:48   23.426        23426
## 4    841        4    1  12 17:22:34   23.251        23251
## 5    841       13    1  13 17:24:10   23.842        23842
## 6    841       22    1  13 17:24:29   23.643        23643
```

```
##   driverId  driverRef number code forename    surname        dob nationality
## 1        1   hamilton     44  HAM    Lewis   Hamilton 1985-01-07     British
## 2        2   heidfeld    \\N  HEI     Nick   Heidfeld 1977-05-10      German
## 3        3    rosberg      6  ROS     Nico    Rosberg 1985-06-27      German
## 4        4     alonso     14  ALO Fernando     Alonso 1981-07-29     Spanish
## 5        5 kovalainen    \\N  KOV   Heikki Kovalainen 1981-10-19     Finnish
## 6        6   nakajima    \\N  NAK   Kazuki   Nakajima 1985-01-11    Japanese
##                                              url
## 1    http://en.wikipedia.org/wiki/Lewis_Hamilton
## 2     http://en.wikipedia.org/wiki/Nick_Heidfeld
## 3      http://en.wikipedia.org/wiki/Nico_Rosberg
## 4   http://en.wikipedia.org/wiki/Fernando_Alonso
## 5 http://en.wikipedia.org/wiki/Heikki_Kovalainen
## 6   http://en.wikipedia.org/wiki/Kazuki_Nakajima
```

```
##   raceId year round circuitId                  name       date     time
## 1      1 2009     1         1 Australian Grand Prix 2009-03-29 06:00:00
## 2      2 2009     2         2  Malaysian Grand Prix 2009-04-05 09:00:00
## 3      3 2009     3        17    Chinese Grand Prix 2009-04-19 07:00:00
## 4      4 2009     4         3    Bahrain Grand Prix 2009-04-26 12:00:00
## 5      5 2009     5         4    Spanish Grand Prix 2009-05-10 12:00:00
## 6      6 2009     6         6     Monaco Grand Prix 2009-05-24 12:00:00
##                                                       url
## 1 http://en.wikipedia.org/wiki/2009_Australian_Grand_Prix
## 2  http://en.wikipedia.org/wiki/2009_Malaysian_Grand_Prix
## 3    http://en.wikipedia.org/wiki/2009_Chinese_Grand_Prix
## 4    http://en.wikipedia.org/wiki/2009_Bahrain_Grand_Prix
## 5    http://en.wikipedia.org/wiki/2009_Spanish_Grand_Prix
## 6     http://en.wikipedia.org/wiki/2009_Monaco_Grand_Prix
```

```
##   circuitId  circuitRef                           name     location   country
## 1         1 albert_park Albert Park Grand Prix Circuit    Melbourne Australia
## 2         2      sepang   Sepang International Circuit Kuala Lumpur  Malaysia
## 3         3     bahrain  Bahrain International Circuit       Sakhir   Bahrain
## 4         4   catalunya Circuit de Barcelona-Catalunya     Montmeló     Spain
## 5         5    istanbul                  Istanbul Park     Istanbul    Turkey
## 6         6      monaco              Circuit de Monaco  Monte-Carlo    Monaco
##         lat       lng alt
## 1 -37.84970 144.96800  10
## 2   2.76083 101.73800  18
## 3  26.03250  50.51060   7
## 4  41.57000   2.26111 109
## 5  40.95170  29.40500 130
## 6  43.73470   7.42056   7
##                                                           url
## 1   http://en.wikipedia.org/wiki/Melbourne_Grand_Prix_Circuit
## 2   http://en.wikipedia.org/wiki/Sepang_International_Circuit
## 3  http://en.wikipedia.org/wiki/Bahrain_International_Circuit
## 4 http://en.wikipedia.org/wiki/Circuit_de_Barcelona-Catalunya
## 5                  http://en.wikipedia.org/wiki/Istanbul_Park
## 6              http://en.wikipedia.org/wiki/Circuit_de_Monaco
```

Combine datasets



```r
head(pit_stops_drivers_circuits_races)
```

```
##   circuitId raceId driverId   driverRef number code forename     surname
## 1         1    841      153 alguersuari    \\N  ALG    Jaime Alguersuari
## 2         1    841       16       sutil     99  SUT   Adrian       Sutil
## 3         1    841        1    hamilton     44  HAM    Lewis    Hamilton
## 4         1    841       10       glock    \\N  GLO     Timo       Glock
## 5         1    841      816    ambrosio    \\N  DAM   Jérôme  d'Ambrosio
## 6         1    841        2    heidfeld    \\N  HEI     Nick    Heidfeld
##          dob nationality
## 1 1990-03-23     Spanish
## 2 1983-01-11      German
## 3 1985-01-07     British
## 4 1982-03-18      German
## 5 1985-12-27     Belgian
## 6 1977-05-10      German
##                                                        url.x stop lap   time.x
## 1             http://en.wikipedia.org/wiki/Jaime_Alguersuari    3  35 17:59:45
## 2                  http://en.wikipedia.org/wiki/Adrian_Sutil    2  37 18:02:15
## 3                http://en.wikipedia.org/wiki/Lewis_Hamilton    1  16 17:28:24
## 4                    http://en.wikipedia.org/wiki/Timo_Glock    1  18 17:33:02
## 5 http://en.wikipedia.org/wiki/J%C3%A9r%C3%B4me_d%27Ambrosio    2  38 18:06:53
## 6                 http://en.wikipedia.org/wiki/Nick_Heidfeld    2  30 17:51:32
##   duration milliseconds year round                name.x       date   time.y
## 1   26.348        26348 2011     1 Australian Grand Prix 2011-03-27 06:00:00
## 2   23.871        23871 2011     1 Australian Grand Prix 2011-03-27 06:00:00
## 3   23.227        23227 2011     1 Australian Grand Prix 2011-03-27 06:00:00
## 4   23.792        23792 2011     1 Australian Grand Prix 2011-03-27 06:00:00
## 5   26.446        26446 2011     1 Australian Grand Prix 2011-03-27 06:00:00
## 6   25.098        25098 2011     1 Australian Grand Prix 2011-03-27 06:00:00
##                                                     url.y  circuitRef
## 1 http://en.wikipedia.org/wiki/2011_Australian_Grand_Prix albert_park
## 2 http://en.wikipedia.org/wiki/2011_Australian_Grand_Prix albert_park
## 3 http://en.wikipedia.org/wiki/2011_Australian_Grand_Prix albert_park
## 4 http://en.wikipedia.org/wiki/2011_Australian_Grand_Prix albert_park
## 5 http://en.wikipedia.org/wiki/2011_Australian_Grand_Prix albert_park
## 6 http://en.wikipedia.org/wiki/2011_Australian_Grand_Prix albert_park
##                           name.y  location   country      lat     lng alt
## 1 Albert Park Grand Prix Circuit Melbourne Australia -37.8497 144.968  10
## 2 Albert Park Grand Prix Circuit Melbourne Australia -37.8497 144.968  10
## 3 Albert Park Grand Prix Circuit Melbourne Australia -37.8497 144.968  10
## 4 Albert Park Grand Prix Circuit Melbourne Australia -37.8497 144.968  10
## 5 Albert Park Grand Prix Circuit Melbourne Australia -37.8497 144.968  10
## 6 Albert Park Grand Prix Circuit Melbourne Australia -37.8497 144.968  10
##                                                         url
## 1 http://en.wikipedia.org/wiki/Melbourne_Grand_Prix_Circuit
## 2 http://en.wikipedia.org/wiki/Melbourne_Grand_Prix_Circuit
## 3 http://en.wikipedia.org/wiki/Melbourne_Grand_Prix_Circuit
## 4 http://en.wikipedia.org/wiki/Melbourne_Grand_Prix_Circuit
## 5 http://en.wikipedia.org/wiki/Melbourne_Grand_Prix_Circuit
## 6 http://en.wikipedia.org/wiki/Melbourne_Grand_Prix_Circuit
```

