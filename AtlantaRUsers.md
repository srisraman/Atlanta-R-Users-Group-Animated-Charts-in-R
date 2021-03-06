Animated Charts in R
================

### Example 1: Gapminder Data

``` r
library(ggplot2)
library(gganimate)
library(gapminder)
# For each of 142 countries, the package provides values for life  expectancy, GDP per capita,
# and population, every five years, from 1952 to 2007.
# head(gapminder)   
```

### Gapminder Data Plot

``` r
p <- ggplot(
  gapminder, 
  aes(x = gdpPercap, y=lifeExp, size = pop, colour = country)) +
  geom_point(show.legend = FALSE, alpha = 0.7) +
  scale_color_viridis_d() +facet_wrap(~continent)+
  scale_size(range = c(2, 12)) +
  scale_x_log10() +labs(x = "GDP per capita", y = "Life expectancy")+
transition_time(year) + ease_aes('linear')+
  labs(title = "Year: {frame_time}")
p
```

![](AtlantaRUsers_files/figure-gfm/unnamed-chunk-2-1.gif)<!-- -->

### Example 2: High School GPA vs. College Graduation GPA Data

``` r
library(ggplot2)
library(gganimate)
gpa <- read.csv("Gradgender.csv")
# str(gpa)
gpa<- na.omit(gpa)
```

### HSGPA vs. GPA by Gender Data Plot

``` r
p <- ggplot(
  gpa, 
  aes(x = HSGPA, y=GPA,colour = Gender))+ ggtitle("HSGPA VS. GPA by Gender")+
  geom_point()+scale_x_continuous(breaks = c(2016:2020))+  xlab(NULL) + ylab(NULL)+theme(legend.position="none")+
  theme(text = element_text(size = 15))+ facet_wrap(~Gender)+ transition_time(Year) + ease_aes('linear')+
  labs(title = "Year: {frame_time}")
p
```

![](AtlantaRUsers_files/figure-gfm/unnamed-chunk-4-1.gif)<!-- -->

### Example 3: Retention & Graduation Rates

``` r
library(ggplot2)
library(gganimate)
library(directlabels)
```

    ## Warning: package 'directlabels' was built under R version 3.6.3

``` r
rg <- read.csv("RGanim2.csv")
# str(rg)
# head(rg)
```

### Retention & Graduation Rates Data Plot

``` r
g <-ggplot(rg,aes(x=Year, y=value,col=variable, group = variable)) +geom_line(size=1)+ geom_point()+
  xlab(NULL) + ylab(NULL) +  scale_color_manual(values=c("black","firebrick")) +ggtitle("Retention & Graduation Rate")+
  geom_dl(aes(label = variable), method = list(dl.trans(x = x + 0.2), "last.points", cex = 1.0)) +
  theme(legend.position="none")+ scale_x_continuous(breaks = c(2010:2020))+ theme(text = element_text(size = 15))+  transition_reveal(Year) + ease_aes('cubic-in-out')
g
```

![](AtlantaRUsers_files/figure-gfm/unnamed-chunk-6-1.gif)<!-- -->
