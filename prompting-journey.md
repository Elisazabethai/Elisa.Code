---
title: "WeatherWise AI Conversation Logs"
author: Elizabeth Mathemabi
format:
  pdf:
    toc: false
    colorlinks: true
  docx:
    toc: false
    highlight-style: github
  html:
    toc: true
    toc-expand: 2
    embed-resources: true
---

# AI Conversation Logbook for WeatherWise Project

This document provides a comprehensive view of five significant AI interactions used throughout the development of the WeatherWise application. Each conversation demonstrates intentional prompting strategies, critical analysis of responses, iteration on ideas, and integration into real-world project components. These logs reflect not only technical support but also deeper problem-solving discussions on structuring code, handling errors, building visualisations, ethical use of AI, and project modularisation.

---

##  Conversation 1: Fetching and Parsing Weather Data

Tool Used: ChatGPT  
Date: 2025-05-18

```
Me: I’m trying to build a weather advisor system that can show current weather using wttr.in. What’s the simplest way to get weather data for a user-given location?

AI: The wttr.in API is ideal for this. You can fetch data in JSON using a URL like: https://wttr.in/Moka?format=j1. Here's a Python snippet:

import requests
url = "https://wttr.in/Moka?format=j1"
response = requests.get(url)
data = response.json()

Me: How do I extract the temperature from that?

AI: You’ll find it inside the "current_condition" key. Use: data["current_condition"][0]["temp_C"]

Me: I want this as a reusable function. What should I watch out for?

AI: You’ll want to handle missing data, bad responses, or timeouts. Include error handling using try/except and make the function flexible by passing location as a parameter.
```

✅ Outcome: Developed a base `get_weather_data()` function with error handling, timeout, and support for different locations.

---

## 🔁 Conversation 2: Error Handling and Input Validation

Tool Used: ChatGPT  
Date: 2025-05-19

```
Me: I want to make my weather fetch function safer. What types of errors should I expect from requests?

AI: Expect:

- Timeout errors (if the server is slow)
- HTTP errors (if API returns 404 or 500)
- Connection errors (no internet)
- JSON decoding errors (malformed responses)

Me: Can you show me how to catch these?

AI: Use this structure:

try:
    response = requests.get(url, timeout=5)
    response.raise_for_status()
    data = response.json()
except requests.exceptions.Timeout:
    print("Timeout occurred")
except requests.exceptions.ConnectionError:
    print("No internet connection")
except requests.exceptions.HTTPError as e:
    print("HTTP error:", e)
except ValueError:
    print("Response is not JSON")
```

Me: I also want to validate the location input. How?

AI: Check if the location is a non-empty string:

if not location.strip():
    return {"error": "Invalid location input."}

✅ Outcome: Function now handles four types of request exceptions and validates user input before calling the API.
```

---

 Conversation 3: Creating Forecast Visualisations

Tool Used: ChatGPT  
Date: 2025-05-20

```
Me: I want to create a visual representation of the weather forecast over three days. What Python tools should I use?

AI: Use matplotlib for basic plots or seaborn for styled visuals. If you want interactivity, use Plotly.

Me: Let’s do it with matplotlib for now.

AI: Extract max/min temps and dates, then:

import matplotlib.pyplot as plt

dates = ["2025-04-21", "2025-04-22", "2025-04-23"]
max_temps = [28, 30, 27]
min_temps = [21, 20, 19]

plt.plot(dates, max_temps, label='Max Temp (°C)', marker='o')
plt.plot(dates, min_temps, label='Min Temp (°C)', marker='x')
plt.title("3-Day Forecast")
plt.xlabel("Date")
plt.ylabel("Temperature")
plt.legend()
plt.grid(True)
plt.show()

Me: What if I want to visualise precipitation chance?

AI: Add a secondary y-axis using twinx():

ax2 = ax1.twinx()
ax2.plot(dates, precip, color='blue', linestyle='--', label="Precipitation (%)")
```

✅ Outcome: Developed clear and informative 3-day forecast charts for temperature and precipitation.
```

---

##  Conversation 4: Structuring Code and Modular Design

Tool Used: ChatGPT  
Date: 2025-05-21

```
Me: My notebook is getting long and messy. I want to structure my project better. How should I divide my code?

AI: Create separate Python modules:

- weather_api.py → for fetching and parsing data
- visualisation.py → for plotting
- question_parser.py → for natural language
- menu.py → for the user interface logic

Me: How do I call them in a notebook?

AI: Use import:

from weather_api import get_weather_data
from visualisation import create_temp_plot

Me: What if I want to test the modules individually?

AI: Add this at the end of each file:

if __name__ == "__main__":
    print(get_weather_data("Moka"))

Me: Should I include constants in a config file?

AI: Yes. Example:

# config.py
API_URL = "https://wttr.in"

Then in your file:
from config import API_URL

✅ Outcome: Code was refactored into 4 reusable modules with clean imports and better maintainability.
```

---

##  Conversation 5: AI Use Reflection and Ethics

**Tool Used:** ChatGPT  
**Date:** 2025-05-22

```
Me: I need to write about how I used AI tools like ChatGPT in my WeatherWise project. Where do I start?

AI: Begin with a summary of how often you used AI and what for—code help, troubleshooting, planning structure, etc.

Me: I used it mainly to check my API calls, design the menu system, and get tips for visualisation. I also asked for follow-ups to improve my functions.

AI: Good. Mention how you used AI responsibly. Did you rely on it entirely or did you evaluate and rewrite suggestions?

Me: I adapted every snippet and made sure I understood it.

AI: Excellent. You can write:

“I used ChatGPT to brainstorm ideas and check Python syntax, but I always validated the logic and edited code to match my style and project goals.”

Me: What ethical concerns should I include?

AI: Include:

- Giving credit to AI tools
- Avoiding blind trust
- Double-checking outputs to avoid spreading wrong info
- Ensuring code is original and personalised

✅ Outcome: Developed a clear, ethical reflection on the role of AI in my learning and development workflow.
```

---

# ✅ Summary

These five conversations illustrate a consistent and reflective use of AI in the WeatherWise project. From API usage and data handling to visualisation and ethical reflection, each interaction was designed to support learning, improve code, and demonstrate thoughtful application of AI tools.
