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
<img width="900" alt="image" src="https://github.com/user-attachments/assets/2c1ec897-b773-46a4-a36d-6d5f55d984a5" />


# Want to know the number of available and unavailable rooms

To analyze the availability of rooms, you can use the following code:

```python
# Count the available and unavailable rooms
calendar.available.value_counts()
```
<img width="882" alt="image" src="https://github.com/user-attachments/assets/45430d92-db4b-426b-8bc1-090c0ce0918f" />

# Calculates the percentage of available (t) and unavailable (f) dates. 📊

```python
availability_percentage = calendar['available'].value_counts(normalize=True) * 100
availability_percentage
```
<img width="905" alt="image" src="https://github.com/user-attachments/assets/4e74240d-aa46-4a30-affe-c1556e60c6d7" />

# Let's Count the Busiest Day! 🚩

Hint: We will be counting the most unavailable days (given by 'f').

To identify the busiest dates, you can use the following code:
```python
# Identify the busiest dates
busiest_dates = calendar[calendar['available'] == 'f']['date'].value_counts()
print("Busiest Dates:")
print(busiest_dates.head())
```
<img width="915" alt="image" src="https://github.com/user-attachments/assets/39a324ac-4876-4b24-9e02-998f253d3389" />

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
<img width="610" alt="image" src="https://github.com/user-attachments/assets/1925effa-d797-41ea-866f-177731caa358" />

# Visualizing the Top 10 Busiest Dates 🚩

To visualize the top 10 busiest dates based on unavailability, you can use the following code:
```python
# Plot the top 10 busiest dates
busiest_dates.head(10).plot(kind='bar', color='darkolivegreen')
plt.title('Top 10 Busiest Dates')
plt.ylabel('Number of Listings Unavailable')
plt.xlabel('Date')
plt.show()
```
<img width="636" alt="image" src="https://github.com/user-attachments/assets/32a333cb-ff30-403b-938f-2a3a8bfd4317" />

# Loading the Data

To load the dataset containing listings information:

```python
import pandas as pd
listings = pd.read_csv('/Users/shatha/Downloads/listings.csv')
```

## Displaying DataFrame Columns 📊

To view the columns of the loaded listings DataFrame, you can use the following code:

```python
listings.columns
```
<img width="857" alt="image" src="https://github.com/user-attachments/assets/80598a54-90d1-4fca-bc3b-20c5172c73ec" />

# Analyzing Average Price by Room Type 💰

To analyze and visualize the average price of listings based on room type, you can use the following code:

```python
import matplotlib.pyplot as plt
price_by_room = listings.groupby('room_type')['price'].mean()
print(price_by_room)

# Plot price by room type
price_by_room.plot(kind='bar', color='darkkhaki')
plt.title('Average Price by Room Type')
plt.ylabel('Average Price')
plt.xlabel('Room Type')

plt.show()
```
<img width="1016" alt="image" src="https://github.com/user-attachments/assets/b5e1a654-6dbf-47f3-bad1-7c175cd8bab3" />

# Identifying the Top 10 Neighborhoods with the Most Listings 🏘️

To find and visualize the neighborhoods with the highest number of listings, you can use the following code:

```python
neighborhood_counts = listings['neighbourhood'].value_counts().head(10)
print("Top 10 Neighborhoods by Listings:")
print(neighborhood_counts)

# Plot neighborhoods with most listings
neighborhood_counts.plot(kind='bar', color='darkkhaki')
plt.title('Top 10 Neighborhoods by Listings')
plt.ylabel('Number of Listings')
plt.xlabel('Neighborhood')
plt.xticks(rotation=90)
plt.show()
```
<img width="945" alt="image" src="https://github.com/user-attachments/assets/a82dc2a4-08c5-4d2a-b298-829cd0821463" />
<img width="971" alt="image" src="https://github.com/user-attachments/assets/ef0480ec-8655-4245-940c-8be180417431" />

# Geographical Distribution of Listings (Price Colored) 🌍

To visualize the geographical distribution of listings, colored by price, you can use the following code:

```python
import matplotlib.pyplot as plt
import seaborn as sns
plt.figure(figsize=(10, 6))
sns.scatterplot(data=listings, x='longitude', y='latitude', hue='price', palette='viridis', size='price', sizes=(10, 200))
plt.title('Geographical Distribution of Listings (Price Colored)')
plt.xlabel('Longitude')
plt.ylabel('Latitude')
plt.show()
```
<img width="954" alt="image" src="https://github.com/user-attachments/assets/9cc68fc2-555b-41a1-9739-965465f4149e" />

# Heatmap Visualization of Los Angeles Listings 🌆

This heatmap displays the density of rental listings in Los Angeles.

## Key Insights 🌈

- **🔥 Hotter Areas (Red/Yellow)**:
  - **High Density**: Areas in red or yellow indicate a higher concentration of listings. 
  - **Popular Locations**: These regions are often in high demand, potentially near tourist attractions or popular neighborhoods.

- **❄️ Colder Areas (Green/Blue)**:
  - **Low Density**: Areas in blue or green indicate fewer listings available.
  - **Less Popular Locations**: These areas may be less sought after or further from key attractions. Lower density could imply less competition, suggesting more affordable options.

- **📍 Density Patterns**:
  - **Clustered Areas**: Clusters of heatmap intensity represent hotspots, often found in high-traffic areas like resorts or urban centers.

Explore the map to find where listings are most abundant! 🗺️

```python
import folium
from folium.plugins import HeatMap

# Filter for relevant columns
LosAngeles_data = listings[['latitude', 'longitude', 'price']]  # Example, you may add more columns

# Create a base map centered around Los Angeles
map_center = [LosAngeles_data['latitude'].mean(), LosAngeles_data['longitude'].mean()]
m = folium.Map(location=map_center, zoom_start=12)

# Prepare the data for the heatmap
heat_data = [[row['latitude'], row['longitude']] for index, row in LosAngeles_data.iterrows()]

# Add the heatmap to the map
HeatMap(heat_data, radius=15).add_to(m)

# Save the map as an HTML file to view in a browser
m.save('LosAngeles_heatmap.html')

# If you're using Jupyter Notebook, you can display the map directly in the notebook:
m
```
<img width="996" alt="image" src="https://github.com/user-attachments/assets/92444ea3-e3e0-461c-b4d2-684b028814fa" />

# What is the relationship between price and availability of listings?

The correlation between price and availability can be positive, indicating that higher-priced listings tend to be less available, or it can be negative, suggesting that lower-priced listings are more frequently available. A dark green color in the heatmap typically represents a strong positive correlation, while lighter colors indicate weaker or negative relationships.

```python
# Calculate the correlation matrix
correlation_matrix = listings[['price', 'availability_365']].corr()

# Create a heatmap to visualize the correlation
plt.figure(figsize=(8, 6))
sns.heatmap(correlation_matrix, annot=True, cmap='YlGn', fmt='.2f', 
            linewidths=0.5, linecolor='darkolivegreen')

plt.title('Correlation Heatmap between Price and Availability')
plt.show()
```
<img width="636" alt="image" src="https://github.com/user-attachments/assets/c4c84791-f747-466f-8864-3d15b562c407" />

# What is the average price distribution among different room types in the listings?

Calculates and visualizes the average price distribution among different room types in listings using a pie chart, showing each type's contribution as a percentage of the total average price.

```python
import pandas as pd
import matplotlib.pyplot as plt

# Load your data
listings = pd.read_csv('/Users/shatha/Downloads/listings.csv')

# Calculate average price by room type
average_price = listings.groupby('room_type')['price'].mean().reset_index()

# Visualization using a pie chart
plt.figure(figsize=(8, 8))
colors = ['darkolivegreen', 'darkkhaki', 'olive']  # Specify colors
plt.pie(average_price['price'], labels=average_price['room_type'], 
        autopct='%1.1f%%', startangle=140, colors=colors)
plt.title('Average Price Distribution by Room Type')
plt.axis('equal')  # Equal aspect ratio ensures that pie is drawn as a circle.
plt.show()
```
<img width="816" alt="image" src="https://github.com/user-attachments/assets/b53351c2-34a1-43ac-a372-3751c1710fd6" />



