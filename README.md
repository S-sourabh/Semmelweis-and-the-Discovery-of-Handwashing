## Project Description
In 1847, the Hungarian physician Ignaz Semmelweis makes a breakthough discovery: He discovers handwashing. Contaminated hands was a major cause of childbed fever and by enforcing handwashing at his hospital he saved hundreds of lives.
In this python project we will reanalyze the medical data Semmelweis collected. This project assumes that you are familiar with python and pandas DataFrames. You can learn the required skills in these courses:

# Project Tasks
Meet Dr. Ignaz Semmelweis
The alarming number of deaths
Death at the clinics
The handwashing begins
The effect of handwashing
The effect of handwashing highlighted
More handwashing, fewer deaths?
A Bootstrap analysis of Semmelweis hand washing data
The fate of Dr. Semmelweis
.......
# Read in datasets/yearly_deaths_by_clinic.csv and assign it to the variable yearly.
yearly = pd.read_csv("yearly_deaths_by_clinic.csv")
print(yearly.to_string())
# Calculate the proportion of deaths per number of births and store the result in the new column yearly["proportion_deaths"].

yearly["proportion_deaths"] = yearly["deaths"] / yearly["births"]
print(yearly["proportion_deaths"])
print(yearly.to_string())
# Extract the rows from clinic 1 into yearly1 and the rows from clinic 2 into yearly2.
# Print out yearly1.
yearly1 = yearly.iloc[:6,:]
print(yearly1)
yearly2 = yearly.iloc[6:,:]
print(yearly2)
# Plot proportion_deaths by year for the two clinics in a single plot. Use the DataFrame plot method.
# Label the plotted lines using the label argument to plot.
# Save the Axes object returned by the plot method into the variable ax.
# Change the y-axis label to "Proportion deaths".

import pandas as pd
pd.plotting.register_matplotlib_converters()
import matplotlib.pyplot as plt
%matplotlib inline
import seaborn as sns
print("Setup Complete")
ax = yearly1.plot(x="year", y="proportion_deaths",
              label="Clinic 1")
yearly2.plot(x="year", y="proportion_deaths",
         label="Clinic 2", ax=ax)
ax.set_ylabel("Proportion Death")
# Plot proportion_deaths by year for the two clinics in a single plot. Use the DataFrame plot method.
# Label the plotted lines using the label argument to plot.
# Save the Axes object returned by the plot method into the variable ax.
# Change the y-axis label to "Proportion deaths".

import pandas as pd
pd.plotting.register_matplotlib_converters()
import matplotlib.pyplot as plt
%matplotlib inline
import seaborn as sns
print("Setup Complete")
ax = yearly1.plot(x="year", y="proportion_deaths",
              label="Clinic 1")
yearly2.plot(x="year", y="proportion_deaths",
         label="Clinic 2", ax=ax)
ax.set_ylabel("Proportion Death")
# Calculate the proportion of deaths per number of births and store the result in the new column monthly["proportion_deaths"].
monthly["proportion_deaths"] = monthly["deaths"] / monthly["births"]
# Print out the first rows in monthly using the head() method.
print(monthly.head())
# Plot the monthly proportion of deaths for Clinic 1.
# Plot proportion_deaths by date for the monthly date using the DataFrame plot method.
# Save the Axes object returned by the plot method into the variable ax.
# Change the y-axis label to "Proportion deaths"
import pandas as pd
pd.plotting.register_matplotlib_converters()
import matplotlib.pyplot as plt
%matplotlib inline
import seaborn as sns
print("Setup Complete")
ax = monthly.plot(x="date", y="proportion_deaths",
              label="proportion_deaths")
ax.set_ylabel("Proportion Death")
# Make a plot that highlights the effect of handwashing
# Split monthly into before_washing (the rows in monthly before handwashing_start) and after_washing 
# (the rows in monthly at and after handwashing_start).
# Plot proportion_deaths in before_washing and after_washing into the same plot. Use the DataFrame plot method.
# Label the plotted lines using the label argument to plot.
# Save the Axes object returned by the plot method into the variable ax.
# Change the y-axis label to "Proportion deaths".

handwashing_start = pd.to_datetime('1847-06-01')

before_washing = monthly[monthly.date < handwashing_start]
after_washing = monthly[monthly.date > handwashing_start]
#at_washing = monthly[
 # monthly["date"] == handwashing_start]
#print(at_washing)
ax = before_washing.plot(x = "date", y = "proportion_deaths", label = "before_handwashing")
after_washing.plot(x = "date", y = "proportion_deaths", label = "after_handwashing", ax = ax)
ax.set_ylabel("proportion_deaths")
# Calculate the average reduction in proportion of deaths due to handwashing.
# Select the column proportion_deaths in before_washing and put it into before_proportion.
# Do the same for proportion_deaths in after_washing and put it into after_proportion.
# Calculate the difference in mean monthly proportion of deaths as mean after_proportion minus mean before_proportion.

before_proportion = before_washing ["proportion_deaths"]
after_proportion = after_washing ["proportion_deaths"]
mean_diff = after_proportion.mean() - before_proportion.mean()
print(mean_diff)
# Make a bootstrap analysis of the difference in mean monthly proportion of deaths.
# boot_before and boot_after should be sampled with replacement from before_proportion and after_proportion.
# Append 3000 bootstrapped differences in means to boot_mean_diff.
# Calculate a 95% confidence_interval as the 2.5% and 97.5% quantiles of boot_mean_diff.

from numpy import percentile
# A bootstrap analysis of the reduction of deaths due to handwashing
boot_mean_diff = []
for i in range(3000):
    boot_before = before_proportion.sample(frac=1, replace=True)
    boot_after = after_proportion.sample(frac=1, replace=True)
    boot_mean_diff.append(boot_after.mean() - boot_before.mean())

# Calculating a 95% confidence interval from boot_mean_diff 
confidence_interval = percentile(boot_mean_diff, [2.5, 97.5])
print(confidence_interval)
# Given the data Semmelweis collected, is it True or False that doctors should wash their hands?
doctors_should_wash_their_hands = True 
