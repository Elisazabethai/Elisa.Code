# Before/After Example: Natural Language Interface – Asking Questions About the Weather

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
Build a simple natural language input feature where the user can type a question and the program gives back a weather response.
```

## Initial AI-Generated Code (Before)

```python
def respond_to_question(question):
    if "temperature" in question:
        return "The temperature is 25°C"
    elif "rain" in question:
        return "There is a chance of rain today."
    else:
        return "Sorry, I don't understand the question."
```

## My Analysis of the Initial Code

The code is a basic keyword match, which is too limited:

1. It doesn't use any real weather data—just hardcoded responses.
2. It can only understand a few exact keywords.
3. It doesn't handle variations in natural language well.
4. There's no input cleaning or parsing, making it fragile.
5. It doesn’t guide the user or adapt to different intents.

## My Follow-up Prompt

```
Please improve this natural language interface to:

1. Accept questions like "Will it rain tomorrow in Moka?" or "What’s the temperature in Port Louis?"
2. Extract intent and location using basic keyword parsing or regex.
3. Call the weather function I created earlier to get real data.
4. Respond in complete, friendly sentences using real weather info.
5. Handle invalid or unclear questions gracefully.
```

## Improved AI-Generated Code (After)

```python
import re

def answer_weather_question(question, fetch_weather_func):
    """
    Respond to a weather-related question in plain English.

    Args:
        question (str): User's natural language weather question.
        fetch_weather_func (function): Function to get weather data.

    Returns:
        str: Friendly response with actual weather info or clarification prompt.
    """
    if not question or not isinstance(question, str):
        return "Please ask a valid question about the weather."

    question = question.lower()
    location_match = re.search(r"in ([a-zA-Z ]+)", question)
    location = location_match.group(1).strip() if location_match else None

    if "temperature" in question and location:
        data = fetch_weather_func(location)
        if data:
            return f"The current temperature in {location.title()} is {data['temperature_C']}°C."
        else:
            return f"Sorry, I couldn't retrieve the weather for {location.title()}."

    elif "rain" in question and location:
        data = fetch_weather_func(location)
        if data:
            return f"In {location.title()}, it's currently {data['weather_desc'].lower()} with {data['humidity']}% humidity. Better carry an umbrella!"
        else:
            return f"I couldn’t get the rain forecast for {location.title()} right now."

    else:
        return "I'm not sure what you're asking. Try something like: 'Will it rain in Moka?' or 'What's the temperature in Port Louis?'"
```

## Why My Prompting Strategy Was Effective

I asked for:

- Integration with real weather data (not hardcoded responses)
- Support for flexible, natural questions
- Better user experience with helpful error messages
- Clear and accurate outputs that sound human

The new function combines parsing, regex, logic, and my earlier API function to simulate a simple AI assistant. It’s more useful and much closer to how a real user would ask questions, making the feature practical and interactive.
