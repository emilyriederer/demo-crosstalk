library(RSocrata)
library(dplyr)
library(lubridate)
library(tidyr)

# pull data ----
trips <- read.socrata("https://data.cityofchicago.org/resource/5neh-572f.json")
stations <- read.socrata("https://data.cityofchicago.org/resource/8pix-ypme.json")

# clean data ----
## subset trips to appropriate timeframe
## recase data
## recode station_name to be consistent across datasets
## rename vbls for usability
trips <- trips[trips$date > "2018-12-31", ]
trips$rides <- as.numeric(trips$rides)
stations <-   transmute(stations, 
                        station_id = map_id,
                        station_name,
                        lat = as.numeric(location.latitude), 
                        lon = as.numeric(location.longitude)) %>% 
  group_by(station_id, station_name) %>%
  summarize_at(vars(lat, lon), mean)
trips <- filter(trips, station_id %in% stations$station_id)

# wrangle summary stats ----
trips_yoy <-
  trips %>%
  rename(station_name = stationname) %>%
  mutate(
    year = year(date),
    mnth = month(date),
    wday = wday(date, week_start = 1),
    wpart = ifelse(wday < 6, "wday", "wend")
  ) %>%
  filter(year >= 2019, mnth == 4) %>%
  group_by(station_name, station_id, year, wpart) %>%
  summarize(rides = sum(rides)) %>%
  pivot_wider(
    names_from = c(year, wpart), 
    names_prefix = "year_", 
    values_from = rides
  ) %>%
  mutate(
    year_2019 = year_2019_wday + year_2019_wend,
    year_2020 = year_2020_wday + year_2020_wend,
    pct_change = (year_2020 - year_2019) / year_2019,
    prop_wend_2019 = year_2019_wend / year_2019 ,
    prop_wend_2020 = year_2020_wend / year_2020
  )

# take a smaller sample ----
set.seed(925)

trips_yoy_sub <-
  trips_yoy %>%
  group_by(bin = round(pct_change, 1)) %>%
  sample_n(4) %>%
  ungroup() %>%
  select(-bin)

stations_sub <- filter(stations, station_id %in% trips_yoy_sub$station_id)

saveRDS(trips_yoy_sub, "data/trips_apr.rds")
saveRDS(stations_sub, "data/stations.rds")

