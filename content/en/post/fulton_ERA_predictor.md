---
#date: 2021-04-09T10:58:08-04:00
description: "Description"
featured_image: "/images/fulton.png"
#tags: ["scene"]
title: "Predicting Housing Assistance Recipients"
---


**Goal**: Develop a predictor for recipients of the Emergency Rent and Utility Assistance program in Fulton County.

**Results**: A logistic regression and gradient boosting classifier that are 77% and 78% accurate on the test data set, respectively, with a geographical interpretable logistic regression coefficients. A heatmap interpretation of these coefficients corresponding to the location data is also implemented through the google maps python package.


## Useful Links

Check out the  to see the code for the project described below.

Some useful links:
* [The GitHub Repo](https://github.com/jcummingsutk/fulton_county_ERA_applications)

* [The Jupyter Notesbook](https://github.com/jcummingsutk/fulton_county_ERA_applications/blob/master/notebook.ipynb)

* [Emergency Rent Program Details](https://www.fultoncountyga.gov/covid-19/rental-assistance)

* [Additional Program Info](https://sharefulton.fultoncountyga.gov/stories/s/Emergency-Rental/22ag-mzc6)

* [Dataset](https://sharefulton.fultoncountyga.gov/Health-Human-Services/Neighborly-ERA-Applications/std8-6vc9)

## Discussion

The Emergency Rent and Utility Assistance (ERA) program is a program throughout the united states that assists families that are in need of emergency assistance for rent and utilities resulting from the COVID-19 pandemic. Residents have to meet eligibility requirements by the federal government, including

* One or more individuals within the household has qualified for unemployment benefits or experienced a reduction in household income, incurred significant costs, or experienced other financial hardship due, directly or indirectly, to the COVID-19 outbreak;
* One or more individuals within the household can demonstrate a risk of experiencing homelessness or housing instability; and
* The household’s income is at or below 80% of the area median income.

An initial exploration of the data shows that when the payment program pays out, it takes on average 100 days for the person to get the money. This is a long time to wait for someone who is struggling due to the pandemic!

With the above details in mind, this project aims to answer the question will I receive assistance from the ERA program?

Below are some links and discussion of the 77% and 78% accurate logistic regression and gradient boosting classifiers that is built for the ERA program applicants.

There are a number of oddities in these data. I have contacted the data set owner to try to gain insight into the oddities, but have not received a reply. Also, the documentation is very poor. There are columns which are unclear. For example, there is a column for funding total amount, total assistance approved, and ams amount (which is the amount of the check given) and they all can differ from one another. Additionally, both the data analysis and the logistic regression predictor indicate those with a lower housing ami ratio (ratio of their rent to average locally) have a smaller chance of receiving aid. Why? People with less money likely need more aid. My hypothesis that could explain this is that there are other data that are not included that are influencing the decision. For example, there is no data indicating a recent job loss. If one lost their job and had higher rent requirements, then perhaps they would likely be approved for aid. However, if someone still kept their job and had low rent requirements, perhaps this program is not applicable to them.

There are some insights that align nicely with reality. In the data analysis and in the logistic regression predictor, higher household size indicates a larger chance of receiving aid. Also, the program specifically mentions that this aid is for non-Atlanta residents in the Fulton county area (much of Fulton county contains Atlanta), and the data and the logistic regression predictor both reflect this fact.

Also optimistically we find that the logistic regression coefficients are large in magnitude for much of the location data. On visualizing this with a heatmap, we find that the areas with the higher coefficients correspond to parts of the poorer regions of the area.

All of this being said, the classifiers, logistic regression and gradient boosting trees, are 77% and 78% accurate respectively.

I had planned on making these classifiers available publicly through a flask application as I did in my [diabetes classifier](https://github.com/jcummingsutk/diabetes_ml_classifier), as I think it would be extremely helpful to an applicant to have some prediction on whether they will receive aid at the moment of application rather than have to wait months. However, until further clarification on why lower income applicants are less likely to receive aid, I hesitate to do so.

# Figures from this project

Here is a picture of Fulton County, for reference
![Fulton County](https://github.com/jcummingsutk/fulton_county_ERA_applications/blob/master/img/fulton.png)

Below you find a heatmap of the lat/long locations with the higher logistic regression coefficients in red, indicating a higher likelihood of aid received In the next cell a map of the greater atlanta area's richer and poorer neighborhoods. Firstly, our heatmap outlines the fulton county area, as expected. More importantly, we see from our heatmap that the poorer areas are more likely to receive aid, as they have the higher coefficients indicated by the more intense red coloring, and that one is less likely to receive aid if they are an applicant from the altlanta area, as the city of atlanta has its own ERA program, indicated by the light green shade.

![Heatmap of Logistic Regression Coefficients](/images/fulton_heatmap.png)

Image showing righer and poorer neighborhoods, with poorer in blue and richer in red. Notice how the general blue areas in Fulton county line up with the red areas. Of course, the blue areas outside of Fulton do not show up on the heatmap, as this data is only for Fulton county.

![Rich and Poor Neighborhoods of Atlanta](/images/high_low_income_area.jpg)
