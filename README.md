import pandas as pd
import plotly.express as px

# Step 1: Define major cities and their coordinates (latitude, longitude)
cities_data = {
    'City': ['Delhi', 'Mumbai', 'Kolkata', 'Chennai', 'Bengaluru', 'Hyderabad', 'Ahmedabad', 'Pune', 'Jaipur', 'Lucknow'],
    'Latitude': [28.6139, 19.0760, 22.5726, 13.0827, 12.9716, 17.3850, 23.0225, 18.5204, 26.9124, 26.8467],
    'Longitude': [77.2090, 72.8777, 88.3639, 80.2707, 77.5946, 78.4867, 72.5714, 73.8567, 75.7873, 80.9462],
    'Value': [0]*10  # Default 0; user will input values
}

df = pd.DataFrame(cities_data)

# Step 2: Take user input for city values
print("Enter a number (e.g. 0–100) for each city to represent its intensity:")
for i in range(len(df)):
    try:
        val = float(input(f"{df.loc[i, 'City']}: "))
    except ValueError:
        val = 0
    df.loc[i, 'Value'] = val

# Step 3: Create the map
fig = px.scatter_geo(
    df,
    lat="Latitude",
    lon="Longitude",
    text="City",
    color="Value",
    color_continuous_scale="Reds",  # Darker red = higher value
    size="Value",
    projection="mercator",
    title="📍 India City Intensity Map (Higher Value = Darker Shade)",
    scope="asia"
)

# Step 4: Adjust the map view for India
fig.update_geos(
    fitbounds="locations",
    visible=False
)

# Step 5: Display the map
fig.show()
