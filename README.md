
from tkinter import messagebox
import requests

def get_weather(api_key, city):
    base_url = f"http://api.openweathermap.org/data/2.5/weather?q={city}&appid={api_key}&units=metric"
    response = requests.get(base_url)
    weather_data = response.json()
    return weather_data

def show_weather():
    api_key = "a999a8cd7ed6bd9b8e90d4c6f91646a4"  # Replace with your API key
    city = city_entry.get()
    weather_data = get_weather(api_key, city)

    if 'main' in weather_data:
        weather_label.config(text=f"Weather in {city}: {weather_data['weather'][0]['description']}")
        temp_label.config(text=f"Temperature: {weather_data['main']['temp']}°C")
        feels_like_label.config(text=f"Feels like: {weather_data['main']['feels_like']}°C")
        humidity_label.config(text=f"Humidity: {weather_data['main']['humidity']}%")
    else:
        messagebox.showerror("Error", "Failed to retrieve weather data")

root = tk.Tk()
root.title("Weather App")

city_label = tk.Label(root, text="Enter City:")
city_label.pack()

city_entry = tk.Entry(root)
city_entry.pack()

get_weather_button = tk.Button(root, text="Get Weather", command=show_weather)
get_weather_button.pack()

weather_label = tk.Label(root, text="")
weather_label.pack()

temp_label = tk.Label(root, text="")
temp_label.pack()

feels_like_label = tk.Label(root, text="")
feels_like_label.pack()

humidity_label = tk.Label(root, text="")
humidity_label.pack()

root.mainloop()
