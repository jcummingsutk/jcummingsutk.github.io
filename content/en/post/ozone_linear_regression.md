---
#date: 2021-04-09T10:58:08-04:00
#description: ""
featured_image: "/images/ozone_splash.jpg"
#tags: ["scene"]
title: "Modeling Ozone Pollution Using Polynomial Ridge Regression, Flask API available via AWS elastic beanstalk"
---
Most of us probably remember learning about the protection that the ozone layer in the upper atmosphere lends us. However, ground level ozone has well documented negative effects. Those with Asthma are particularly at risk to it [[1]](https://www.epa.gov/ground-level-ozone-pollution/ground-level-ozone-basics). Denver has one of the worst levels of ground level ozone in the united states [[2]](https://www.denverpost.com/2021/06/16/denver-fortcollins-worst-cities-air-pollution/). It is well known that ozone is greatly affected by pollutants emitted by cars, power plants, refineries, etc. in the presence of sunlight [[3]](https://www.epa.gov/ground-level-ozone-pollution/ground-level-ozone-basics#:~:text=This%20happens%20when%20pollutants%20emitted,high%20levels%20during%20colder%20months.).

**Goal**: To develop an accurate ridge polynomial regression model to predict the amount of ozone in the air.

The results from this project are deployed as a REST api on AWS elastic beanstalk. You can hit the api by using, for example, [postman](https://www.postman.com/) to sent a GET api request to [Denverozonepredictor-env.eba-phyjudqm.us-east-1.elasticbeanstalk.com](Denverozonepredictor-env.eba-phyjudqm.us-east-1.elasticbeanstalk.com). It expects a json dictionary such as
```json
{
    "temp": 100,
    "humidity": 0,
    "windspeed": 5,
    "month": 7,
    "sea_level_pressure": 1000.8,
    "hour": 15,
    "is_weekend": 0
}
```
variable descriptions:

* temp: temperature in F
* humidity: relative humidity percentage
* windspeed: wind speed in mph
* month: numeric value of the months
* sea_level_pressure: pressure in millibars
* hour: hour of the day (0-23)
* is_weekend: 0 if not the weekend, 1 if it is.

Useful links:
[GitHub Page](https://github.com/jcummingsutk/ozone_pollution)

[Jupyter Notebook](https://github.com/jcummingsutk/ozone_pollution/blob/master/notebook.ipynb)

[Ozone Data](https://aqs.epa.gov/aqsweb/airdata/download_files.html#Raw)

[Worst Ranking Ozone Levels](https://www.lung.org/research/sota/city-rankings/most-polluted-cities)

[Historical Weather Data](https://visualcrossing.com/)

[Weather Data Documentation](https://www.visualcrossing.com/resources/documentation/weather-data/weather-data-documentation/)

[Effect of Weekends](https://www.tandfonline.com/doi/full/10.1080/10962247.2012.749312#:~:text=In%20simple%20terms%2C%20the%20ozone,NOx\)%2C%20on%20weekends.)

**Results**: Using historical weather data paired with EPA data on ozone pollutant a fifth degree polynomial regression model with R^2 of 0.76 and a MAE of .0064 and RMSE .0085 ppm on the test set is developed. There is some amount of overfitting on the training set with this model, as the MAE and RMSE on the validation set are .054 and .069 respectively. However, this overfitting is relatively mild and ridge regression does not appear to do any better on the test set. The fifth degree ridge regression model developed has a MAE of .0067 and .0085, and is the model that is implemented on AWS elastic beanstalk as an API.

Possible extensions: A couple improvements I'd like to make is I'd like to capture the tail of this distribution better. The model could be built to more heavily penalize inaccuracies in the higher end of the ozone range, to attempt to be a more conservative predictor. I think that importing a custom loss function to penalize the error made at higher ozone levels could be helpful here. There is also the issue of linear regression models predicting negative ozone levels. However, this is not as concerning to me as we can consider those to be zero.
