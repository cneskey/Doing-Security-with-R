# Tools written in R for doing security

## Cybersecurity data analysis

### Model evaluation
Run this code to:
1. Create a basic random forest classification model.
2. Fit that model to the latest VERIS Community Database data.
3. Test the model's predictive accuracy on using more historical data.
4. Visualize how Action types predicted Time-to-Discovery.

We'll visualize the model's predictive ability by plotting 7 Partial Dependence Plots (PDPs), one for each of the categories of "Action" in the VERIS schema.
Our predictors:    malware, hacking, social, misuse, physical, error, environmental
Our predicted:     Time to Discovery (timeline.discovery.value)

#### More
# [1] http://veriscommunity.net/discovery.html#section-incident-timeline
# [2] https://stephenmilborrow.r-universe.dev/plotmo

Make this:
![image](https://github.com/cneskey/Doing-Security-with-R/assets/4606261/aaf731b0-fcc6-4c40-a1b6-b2ae2e254dd2)


With this:

Or this:
