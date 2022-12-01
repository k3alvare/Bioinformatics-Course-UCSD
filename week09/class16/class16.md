COVID-19 Vaccination Rates Mini-Project
================
Kyle

We will be examining and comparing the Covid-19 vaccination rates in San
Diego.

Start by downloading the most recently dated “Statewide COVID-19
Vaccines Administered by ZIP Code” CSV file.

``` r
# Import vaccination data
vax <- read.csv("https://data.chhs.ca.gov/dataset/ead44d40-fd63-4f9f-950a-3b0111074de8/resource/ec32eece-7474-4488-87f0-6e91cb577458/download/covid19vaccinesbyzipcode_test.csv")
head(vax)
```

      as_of_date zip_code_tabulation_area local_health_jurisdiction         county
    1 2021-01-05                    91606               Los Angeles    Los Angeles
    2 2021-01-05                    95312                    Merced         Merced
    3 2021-01-05                    91350               Los Angeles    Los Angeles
    4 2021-01-05                    91708            San Bernardino San Bernardino
    5 2021-01-05                    95305                  Tuolumne       Tuolumne
    6 2021-01-05                    91351               Los Angeles    Los Angeles
      vaccine_equity_metric_quartile                 vem_source
    1                              1 Healthy Places Index Score
    2                              1    CDPH-Derived ZCTA Score
    3                              4 Healthy Places Index Score
    4                             NA            No VEM Assigned
    5                             NA            No VEM Assigned
    6                              3 Healthy Places Index Score
      age12_plus_population age5_plus_population tot_population
    1               38210.0                41964          44295
    2                 187.4                  236            276
    3               29940.2                33775          36173
    4                3517.3                 3794             NA
    5                   0.0                    0             NA
    6               27874.9                30641          32711
      persons_fully_vaccinated persons_partially_vaccinated
    1                       14                          482
    2                       NA                           NA
    3                       65                         1225
    4                       NA                           NA
    5                       NA                           NA
    6                       31                          644
      percent_of_population_fully_vaccinated
    1                               0.000316
    2                                     NA
    3                               0.001797
    4                                     NA
    5                                     NA
    6                               0.000948
      percent_of_population_partially_vaccinated
    1                                   0.010882
    2                                         NA
    3                                   0.033865
    4                                         NA
    5                                         NA
    6                                   0.019688
      percent_of_population_with_1_plus_dose booster_recip_count
    1                               0.011198                  NA
    2                                     NA                  NA
    3                               0.035662                  NA
    4                                     NA                  NA
    5                                     NA                  NA
    6                               0.020636                  NA
      bivalent_dose_recip_count eligible_recipient_count
    1                        NA                       14
    2                        NA                        0
    3                        NA                       65
    4                        NA                        6
    5                        NA                        0
    6                        NA                       31
                                                                   redacted
    1 Information redacted in accordance with CA state privacy requirements
    2 Information redacted in accordance with CA state privacy requirements
    3 Information redacted in accordance with CA state privacy requirements
    4 Information redacted in accordance with CA state privacy requirements
    5 Information redacted in accordance with CA state privacy requirements
    6 Information redacted in accordance with CA state privacy requirements

> Q1. What column details the total number of people fully vaccinated?
> The column that details the total number of people fully vaccinated is
> “persona_fully_vaccinated”.

> Q2. What column details the Zip code tabulation area? The column that
> details the Zip code tabululation area is “zip_code_tabulation_area”.

``` r
head(vax$as_of_date)
```

    [1] "2021-01-05" "2021-01-05" "2021-01-05" "2021-01-05" "2021-01-05"
    [6] "2021-01-05"

``` r
tail(vax$as_of_date)
```

    [1] "2022-11-29" "2022-11-29" "2022-11-29" "2022-11-29" "2022-11-29"
    [6] "2022-11-29"

> Q3. What is the earliest date in this dataset? The earliest date is
> 2021-01-05

> Q4. What is the latest date in this dataset? The latest date is
> 2022-11-22

``` r
skimr::skim(vax)
```

|                                                  |        |
|:-------------------------------------------------|:-------|
| Name                                             | vax    |
| Number of rows                                   | 176400 |
| Number of columns                                | 18     |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_   |        |
| Column type frequency:                           |        |
| character                                        | 5      |
| numeric                                          | 13     |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |        |
| Group variables                                  | None   |

Data summary

**Variable type: character**

| skim_variable             | n_missing | complete_rate | min | max | empty | n_unique | whitespace |
|:--------------------------|----------:|--------------:|----:|----:|------:|---------:|-----------:|
| as_of_date                |         0 |             1 |  10 |  10 |     0 |      100 |          0 |
| local_health_jurisdiction |         0 |             1 |   0 |  15 |   500 |       62 |          0 |
| county                    |         0 |             1 |   0 |  15 |   500 |       59 |          0 |
| vem_source                |         0 |             1 |  15 |  26 |     0 |        3 |          0 |
| redacted                  |         0 |             1 |   2 |  69 |     0 |        2 |          0 |

**Variable type: numeric**

| skim_variable                              | n_missing | complete_rate |     mean |       sd |    p0 |      p25 |      p50 |      p75 |     p100 | hist  |
|:-------------------------------------------|----------:|--------------:|---------:|---------:|------:|---------:|---------:|---------:|---------:|:------|
| zip_code_tabulation_area                   |         0 |          1.00 | 93665.11 |  1817.39 | 90001 | 92257.75 | 93658.50 | 95380.50 |  97635.0 | ▃▅▅▇▁ |
| vaccine_equity_metric_quartile             |      8700 |          0.95 |     2.44 |     1.11 |     1 |     1.00 |     2.00 |     3.00 |      4.0 | ▇▇▁▇▇ |
| age12_plus_population                      |         0 |          1.00 | 18895.04 | 18993.88 |     0 |  1346.95 | 13685.10 | 31756.12 |  88556.7 | ▇▃▂▁▁ |
| age5_plus_population                       |         0 |          1.00 | 20875.24 | 21105.98 |     0 |  1460.50 | 15364.00 | 34877.00 | 101902.0 | ▇▃▂▁▁ |
| tot_population                             |      8600 |          0.95 | 23372.77 | 22628.51 |    12 |  2126.00 | 18714.00 | 38168.00 | 111165.0 | ▇▅▂▁▁ |
| persons_fully_vaccinated                   |     15048 |          0.91 | 13504.90 | 14748.88 |    11 |   887.00 |  8076.00 | 22588.00 |  87207.0 | ▇▃▁▁▁ |
| persons_partially_vaccinated               |     15048 |          0.91 |  1707.77 |  2001.11 |    11 |   167.00 |  1195.00 |  2547.00 |  39228.0 | ▇▁▁▁▁ |
| percent_of_population_fully_vaccinated     |     18834 |          0.89 |     0.55 |     0.25 |     0 |     0.40 |     0.59 |     0.73 |      1.0 | ▃▃▆▇▃ |
| percent_of_population_partially_vaccinated |     18834 |          0.89 |     0.08 |     0.09 |     0 |     0.05 |     0.06 |     0.08 |      1.0 | ▇▁▁▁▁ |
| percent_of_population_with_1\_plus_dose    |     19739 |          0.89 |     0.62 |     0.25 |     0 |     0.46 |     0.65 |     0.79 |      1.0 | ▂▂▅▇▆ |
| booster_recip_count                        |     70611 |          0.60 |  5643.35 |  6858.00 |    11 |   281.00 |  2585.00 |  9377.00 |  58376.0 | ▇▂▁▁▁ |
| bivalent_dose_recip_count                  |    157094 |          0.11 |  1770.66 |  2315.50 |    11 |   117.00 |   778.00 |  2643.75 |  18815.0 | ▇▁▁▁▁ |
| eligible_recipient_count                   |         0 |          1.00 | 12345.64 | 14582.42 |     0 |   468.00 |  5851.00 | 21198.25 |  86706.0 | ▇▂▁▁▁ |

> Q5. How many numeric columns are in this dataset? There are 13 numeric
> columns in this dataset

``` r
sum(is.na(vax$persons_fully_vaccinated))
```

    [1] 15048

> Q6. Note that there are “missing values” in the dataset. How many NA
> values there in the persons_fully_vaccinated column? According to my
> data set there is 14921 missing values, however in the lab sheet there
> is 15440 missing.

> Q7. What percent of persons_fully_vaccinated values are missing (to 2
> significant figures)? In my data set there is 8.54% percent of
> persona_fully_vaccinated values missing. In the lab sheet there is
> 8.93%

``` r
nrow(vax)
```

    [1] 176400

``` r
14921/174636 * 100
```

    [1] 8.544057

> Q8. \[Optional\]: Why might this data be missing? Data might be
> missing because the person might of requested to opt out of their
> information being studied.

## Working with Dates

Using the `lubridate` package, dates and times become easier to work
with.

``` r
library(lubridate)
```

    Loading required package: timechange


    Attaching package: 'lubridate'

    The following objects are masked from 'package:base':

        date, intersect, setdiff, union

``` r
today()
```

    [1] "2022-12-01"

``` r
# Specify that we are using the year-month-day format
vax$as_of_date <- ymd(vax$as_of_date)
```

Now we can do math with dates. For example: How many days have passed
since the first vaccination reported in this dataset?

``` r
today() - vax$as_of_date[1]
```

    Time difference of 695 days

Using the last and the first date value we can now determine how many
days the dataset span.

``` r
vax$as_of_date[nrow(vax)] - vax$as_of_date[1]
```

    Time difference of 693 days

> Q9. How many days have passed since the last update of the dataset?
> According to my dataset only 3 days have passed, whilst the lab sheet
> 6 days have passed.

> Q10. How many unique dates are in the dataset (i.e. how many different
> dates are detailed)? 99 unique dates according to my dataset, whilst
> the lab sheet is 97 unique dates.

``` r
(unique(vax$as_of_date))
```

      [1] "2021-01-05" "2021-01-12" "2021-01-19" "2021-01-26" "2021-02-02"
      [6] "2021-02-09" "2021-02-16" "2021-02-23" "2021-03-02" "2021-03-09"
     [11] "2021-03-16" "2021-03-23" "2021-03-30" "2021-04-06" "2021-04-13"
     [16] "2021-04-20" "2021-04-27" "2021-05-04" "2021-05-11" "2021-05-18"
     [21] "2021-05-25" "2021-06-01" "2021-06-08" "2021-06-15" "2021-06-22"
     [26] "2021-06-29" "2021-07-06" "2021-07-13" "2021-07-20" "2021-07-27"
     [31] "2021-08-03" "2021-08-10" "2021-08-17" "2021-08-24" "2021-08-31"
     [36] "2021-09-07" "2021-09-14" "2021-09-21" "2021-09-28" "2021-10-05"
     [41] "2021-10-12" "2021-10-19" "2021-10-26" "2021-11-02" "2021-11-09"
     [46] "2021-11-16" "2021-11-23" "2021-11-30" "2021-12-07" "2021-12-14"
     [51] "2021-12-21" "2021-12-28" "2022-01-04" "2022-01-11" "2022-01-18"
     [56] "2022-01-25" "2022-02-01" "2022-02-08" "2022-02-15" "2022-02-22"
     [61] "2022-03-01" "2022-03-08" "2022-03-15" "2022-03-22" "2022-03-29"
     [66] "2022-04-05" "2022-04-12" "2022-04-19" "2022-04-26" "2022-05-03"
     [71] "2022-05-10" "2022-05-17" "2022-05-24" "2022-05-31" "2022-06-07"
     [76] "2022-06-14" "2022-06-21" "2022-06-28" "2022-07-05" "2022-07-12"
     [81] "2022-07-19" "2022-07-26" "2022-08-02" "2022-08-09" "2022-08-16"
     [86] "2022-08-23" "2022-08-30" "2022-09-06" "2022-09-13" "2022-09-20"
     [91] "2022-09-27" "2022-10-04" "2022-10-11" "2022-10-18" "2022-10-25"
     [96] "2022-11-01" "2022-11-08" "2022-11-15" "2022-11-22" "2022-11-29"

## Working with ZIP codes

In R we can use the zipcodeR package to make working with these codes
easier. For example, let’s install and then load up this package and to
find the centroid of the La Jolla 92037 (i.e. UC San Diego) ZIP code
area.

``` r
library(zipcodeR)
```

``` r
geocode_zip('92037')
```

    # A tibble: 1 × 3
      zipcode   lat   lng
      <chr>   <dbl> <dbl>
    1 92037    32.8 -117.

Calculate the distance between the centroids of any two ZIP codes in
miles, e.g.

``` r
zip_distance('92037','92109')
```

      zipcode_a zipcode_b distance
    1     92037     92109     2.33

More usefully, we can pull census data about ZIP code areas (including
median household income etc.). For example:

``` r
reverse_zipcode(c('92037', "92109") )
```

    # A tibble: 2 × 24
      zipcode zipcode_…¹ major…² post_…³ common_c…⁴ county state   lat   lng timez…⁵
      <chr>   <chr>      <chr>   <chr>       <blob> <chr>  <chr> <dbl> <dbl> <chr>  
    1 92037   Standard   La Jol… La Jol… <raw 20 B> San D… CA     32.8 -117. Pacific
    2 92109   Standard   San Di… San Di… <raw 21 B> San D… CA     32.8 -117. Pacific
    # … with 14 more variables: radius_in_miles <dbl>, area_code_list <blob>,
    #   population <int>, population_density <dbl>, land_area_in_sqmi <dbl>,
    #   water_area_in_sqmi <dbl>, housing_units <int>,
    #   occupied_housing_units <int>, median_home_value <int>,
    #   median_household_income <int>, bounds_west <dbl>, bounds_east <dbl>,
    #   bounds_north <dbl>, bounds_south <dbl>, and abbreviated variable names
    #   ¹​zipcode_type, ²​major_city, ³​post_office_city, ⁴​common_city_list, …

Let’s now focus in on the San Diego County area by restricting ourselves
first to `vax$county == "San Diego"` entries

``` r
# Subset to San Diego county only areas
sd <- vax[ vax$county == "San Diego" , ]
```

Using dplyr the code would look like this:

``` r
library(dplyr)
```


    Attaching package: 'dplyr'

    The following objects are masked from 'package:stats':

        filter, lag

    The following objects are masked from 'package:base':

        intersect, setdiff, setequal, union

``` r
sd <- filter(vax, county == "San Diego")

nrow(sd)
```

    [1] 10700

Using dplyr is often more convenient when we are subsetting across
multiple criteria - for example all San Diego county areas with a
population of over 10,000.

``` r
sd.10 <- filter(vax, county == "San Diego" &
                age5_plus_population > 10000)
```

> Q11. How many distinct zip codes are listed for San Diego County 107
> distinct zip codes are listed for San Diego County.

``` r
length(unique(sd$zip_code_tabulation_area))
```

    [1] 107

> Q12. What San Diego County Zip code area has the largest 12 +
> Population in this dataset? 92154 has the highest 12 + population in
> this dataset.

``` r
which.max(sd.10$age12_plus_population)
```

    [1] 57

``` r
sd.10[32,]
```

       as_of_date zip_code_tabulation_area local_health_jurisdiction    county
    32 2021-01-05                    92102                 San Diego San Diego
       vaccine_equity_metric_quartile                 vem_source
    32                              1 Healthy Places Index Score
       age12_plus_population age5_plus_population tot_population
    32               37042.3                41033          44010
       persons_fully_vaccinated persons_partially_vaccinated
    32                       20                         1287
       percent_of_population_fully_vaccinated
    32                               0.000454
       percent_of_population_partially_vaccinated
    32                                   0.029243
       percent_of_population_with_1_plus_dose booster_recip_count
    32                               0.029697                  NA
       bivalent_dose_recip_count eligible_recipient_count
    32                        NA                       20
                                                                    redacted
    32 Information redacted in accordance with CA state privacy requirements

``` r
sd.toplot <- filter(vax, county == "San Diego" &
                      as_of_date == "2022-11-15")
```

> Q13. What is the overall average “Percent of Population Fully
> Vaccinated” value for all San Diego “County” as of “2022-11-15”? The
> overal average of percent in my dataset is 0.7369099 but in the lab it
> is “0.738176464646465

``` r
mean(na.omit(sd.toplot$percent_of_population_fully_vaccinated))
```

    [1] 0.7370352

> Q14. Using either ggplot or base R graphics make a summary figure that
> shows the distribution of Percent of Population Fully Vaccinated
> values as of “2022-11-15”?

``` r
library(ggplot2)

##ggplot(sd.toplot, aes(+
     #    geom_bar(stat = "bin")
```
