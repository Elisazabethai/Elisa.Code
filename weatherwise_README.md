
# Elizabeth's WeatherWise App 🌈

Welcome to **WeatherWise** — your offline weather advisor that blends simple Python, mock data, and nifty visuals to keep you weather-wise without needing an internet connection!

---

## What Is WeatherWise?

WeatherWise is a terminal-based Python app that simulates weather forecasting using mock data. It allows you to:

- Ask natural language weather questions about rain, temperature, or wind.  
- Visualize temperature trends with a slick line chart.  
- Visualize rain volume over time with an easy-to-read bar chart.

Perfect for learning, demos, or when you just wanna vibe offline.

---

## How The Code Works — Key Components

### 1. Mock Weather Data  
The app uses a static dataset mimicking real weather info:  
- Timestamp (`dt`)  
- Temperature (`temp`)  
- Weather description (`clear sky`, `light rain`, etc.)  
- Wind speed (`speed`)  
- Rain volume over 3 hours (`rain['3h']`)

This lets the app run without calling any live APIs.

### 2. Visualization Functions  
- `create_temperature_visualisation(weather_data)`  
  Plots temperature against time with a hot pink line chart.  

- `create_precipitation_visualisation(weather_data)`  
  Displays rain volume as a blue bar chart, showing mm of rain per 3-hour interval.

Both use **Matplotlib** for clean, colorful visuals.

### 3. Natural Language Processing (NLP)  
- `parse_weather_question(question)` looks for keywords related to rain, temperature, or wind in your questions.  
- `generate_weather_response(parsed_question, weather_data)` creates a relevant answer from the mock data.

This means you can type things like *"Will it rain soon?"* or *"Is it windy today?"* and get a friendly bot reply.

### 4. User Interface (Menu-driven)  
The main menu offers options to:  
- Ask weather questions interactively.  
- View temperature or rain charts.  
- Exit the app gracefully.

You can loop through these options as many times as you want.

---

## How To Run WeatherWise

### Prerequisites  
Make sure you have these installed:

- Python 3.x  
- [Matplotlib](https://matplotlib.org/stable/users/installing.html) (for plotting)  
- [PyInputPlus](https://pypi.org/project/PyInputPlus/) (for input validation and menus)

You can install missing packages via pip:

```bash
pip install matplotlib pyinputplus
```

### Running The App

1. Save the Python script (e.g., `weatherwise.py`).  
2. Open your terminal/command prompt.  
3. Navigate to the directory where the script is saved.  
4. Run the script with:

```bash
python weatherwise.py
```

5. Follow the prompts:  
   - Enter any city name (mock data is static, so any input works).  
   - Use the menu to ask weather questions or view charts.  
   - Type `back` to return to the main menu from the question prompt.  
   - Select "Exit" to close the app.

---

## Why Use WeatherWise?

- **Offline Capable:** No internet required — perfect for practice or demoing data visualizations and NLP basics.  
- **Interactive & Visual:** Combines chat-like questions with colorful charts.  
- **Clean Modular Code:** Easy to customize, extend, or swap out mock data for real APIs in the future.

---


---

## Final Notes

Elizabeth's WeatherWise is more than a demo—it's a learning playground for blending data, visualization, and natural language understanding. Dive in, experiment, and ride the weather waves with style!

---

*Made with 💖 by Elizabeth Mathemabi (Elisa)*  
*Business Information Systems Student, Curtin Mauritius*  
*Aspiring Proverbs 31 Woman & Future Data Analyst*  
*Keep it fly and weather-wise! 🌟*
