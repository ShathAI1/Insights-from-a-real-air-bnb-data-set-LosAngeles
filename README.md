# Insights-from-a-real-air-bnb-data-set-LosAngeles
Python code for insights on Airbnb booking of  LosAngeles. I am using calender and listing cv files

To run the following code you can download the calendar csv file from:
https://data.insideairbnb.com/united-kingdom/england/london/2024-09-06/data/calendar.csv.gz

also the listings from this link:
https://data.insideairbnb.com/united-states/ca/los-angeles/2024-09-04/visualisations/listings.csv

<img width="870" alt="image" src="https://github.com/user-attachments/assets/d7d7fdfc-31c3-4d88-9de5-46c2b6033b82" />

# Loading the Data

Once you have the file, you can use the following code to load the data and analyze room availability:

```python
# Import necessary library
import pandas as pd

# Load the dataset
calendar = pd.read_csv('calendar.csv.gz')
```
## Displaying the Data

To display the entire DataFrame, you can use the data frame name:
```python
calendar
```

# Want to know the number of available and unavailable rooms

To analyze the availability of rooms, you can use the following code:

```python
# Count the available and unavailable rooms
calendar.available.value_counts()
```
# Calculates the percentage of available (t) and unavailable (f) dates. 📊

```python
availability_percentage = calendar['available'].value_counts(normalize=True) * 100
availability_percentage
```
# Let's Count the Busiest Day! 🚩

Hint: We will be counting the most unavailable days (given by 'f').

To identify the busiest dates, you can use the following code:
```python
# Identify the busiest dates
busiest_dates = calendar[calendar['available'] == 'f']['date'].value_counts()
print("Busiest Dates:")
print(busiest_dates.head())
```
# Plot a bar graph to show availability percentage
To visualize the availability percentages, you can use the following code:

```python
import matplotlib.pyplot as plt

# Plot the availability percentages
availability_percentage.plot(kind='bar', color=['darkolivegreen', 'antiquewhite'])
plt.title('Availability Percentages')
plt.ylabel('Percentage')
plt.xlabel('Available (t/f)')
plt.show()
```


