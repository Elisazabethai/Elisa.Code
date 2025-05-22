Before/After Example: User Experience – Intuitive Menu System

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

## Initial Prompt

```
Make a menu so the user can pick what they want to see: current weather, forecast, or exit.
```

## Initial AI-Generated Code (Before)

```python
def show_menu():
    print("1. Current weather")
    print("2. Forecast")
    print("3. Exit")
    choice = input("Enter choice: ")
    return choice
```

## My Analysis of the Initial Code

This version is very basic and has several weaknesses:

1. No input validation—program crashes with invalid input
2. Not user-friendly or interactive
3. No loop to keep the menu running
4. Doesn’t use pyinputplus, which is safer and cleaner
5. Instructions are minimal and unfriendly

## My Follow-up Prompt

```
Please improve this menu system to:

1. Use pyinputplus to get valid input with retries
2. Display friendly and clear instructions
3. Loop the menu until the user exits
4. Call the right weather functions depending on user choice
5. Handle invalid responses with helpful messages
```

## Improved AI-Generated Code (After)

```python
import pyinputplus as pyip

def run_weather_menu(get_weather_func, ask_question_func):
    print("Welcome to WeatherWise ")
    while True:
        print("\nWhat would you like to do?")
        print("1. View current weather")
        print("2. View forecast")
        print("3. Ask a question in natural language")
        print("4. Exit")

        choice = pyip.inputMenu(["1", "2", "3", "4"], numbered=False)

        if choice == "1":
            location = pyip.inputStr("Enter a location (e.g., Moka): ")
            data = get_weather_func(location)
            if data:
                print(f"Current temperature in {location.title()}: {data['temperature_C']}°C")
            else:
                print("Sorry, couldn't retrieve weather data.")

        elif choice == "2":
            location = pyip.inputStr("Enter a location (e.g., Moka): ")
            data = get_weather_func(location, forecast_days=3)
            if data and 'forecast' in data:
                print(f"3-day forecast for {location.title()}:")
                for day in data['forecast']:
                    print(f"{day['date']}: {day['condition']} ({day['min_temp']}–{day['max_temp']}°C)")
            else:
                print("No forecast available.")

        elif choice == "3":
            question = pyip.inputStr("Ask your question (e.g., Will it rain in Moka?): ")
            print(ask_question_func(question, get_weather_func))

        elif choice == "4":
            print("Goodbye! ")
            break
```

## Why My Prompting Strategy Was Effective

I was clear about:

- Which library to use (pyinputplus)
- What UX issues to solve (validation, friendliness, clarity)
- How the menu should behave (loop, call real functions, handle errors)

The result is an intuitive and professional user interface that guides the user, avoids crashes, and connects with the core features of my application.
