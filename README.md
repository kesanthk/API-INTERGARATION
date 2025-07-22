# API-INTERGARATION
import requests
import matplotlib.pyplot as plt
import seaborn as sns
from datetime import datetime

# Set Seaborn style
sns.set(style="whitegrid")

# Replace with your OpenWeatherMap API key
API_KEY = 'your_api_key_here'
CITY = 'Chennai'
URL = f'https://api.openweathermap.org/data/2.5/forecast?q={CITY}&appid={API_KEY}&units=metric'

# Fetch weather forecast data
response = requests.get(URL)
data = response.json()

# Extract useful data
dates = []
temperatures = []
humidities = []
wind_speeds = []

for entry in data['list']:
    dt = datetime.strptime(entry['dt_txt'], "%Y-%m-%d %H:%M:%S")
    temp = entry['main']['temp']
    humidity = entry['main']['humidity']
    wind_speed = entry['wind']['speed']

    dates.append(dt)
    temperatures.append(temp)
    humidities.append(humidity)
    wind_speeds.append(wind_speed)

# Plotting Temperature
plt.figure(figsize=(12, 6))
sns.lineplot(x=dates, y=temperatures, color="tomato")
plt.title(f"Temperature Forecast for {CITY}", fontsize=16)
plt.xlabel("Date and Time")
plt.ylabel("Temperature (°C)")
plt.xticks(rotation=45)
plt.tight_layout()
plt.grid(True)
plt.show()

# Plotting Humidity
plt.figure(figsize=(12, 6))
sns.lineplot(x=dates, y=humidities, color="skyblue")
plt.title(f"Humidity Forecast for {CITY}", fontsize=16)
plt.xlabel("Date and Time")
plt.ylabel("Humidity (%)")
plt.xticks(rotation=45)
plt.tight_layout()
plt.grid(True)
plt.show()

# Plotting Wind Speed
plt.figure(figsize=(12, 6))
sns.lineplot(x=dates, y=wind_speeds, color="limegreen")
plt.title(f"Wind Speed Forecast for {CITY}", fontsize=16)
plt.xlabel("Date and Time")
plt.ylabel("Wind Speed (m/s)")
plt.xticks(rotation=45)
plt.tight_layout()
plt.grid(True)
plt.show()