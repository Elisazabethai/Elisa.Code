# Before/After Example: Weather Data Component – Retrieving and Visualising Weather Data

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
Write a Python function that fetches weather data for a given location using the wttr.in API. The function should return the raw data and include basic error handling.
```

## Initial AI-Generated Code (Before)

```python
def fetch_weather(location):
    import requests
    url = f"https://wttr.in/{location}?format=j1"
    response = requests.get(url)
    return response.json()
```

## My Analysis of the Initial Code

The initial code works to get data but has several weaknesses:

1. No error handling for failed requests or invalid responses, which may cause crashes.
2. No input validation for the location parameter.
3. It returns the raw JSON data, which is complex and difficult to use directly.
4. No timeout setting, risking the program hanging if the API is slow.
5. No explanation or documentation to guide users on how to use the function.

## My Follow-up Prompt

```
Please improve this function to:

1. Validate that the location is a non-empty string.
2. Add error handling for network errors and bad responses.
3. Include a timeout of 10 seconds on the API request.
4. Parse the API response to return only the current temperature, weather description, and humidity.
5. Document the function with a clear docstring explaining parameters and return values.
```

## Improved AI-Generated Code (After)

```python
def fetch_weather(location):
    """
    Get current weather information for a specified location from wttr.in.

    Args:
        location (str): Name of the city or location.

    Returns:
        dict or None: Dictionary with temperature (C), weather description, and humidity,
                      or None if an error occurs.
    """
    import requests

    if not isinstance(location, str) or not location.strip():
        print("Error: Location must be a non-empty string.")
        return None

    url = f"https://wttr.in/{location.strip()}?format=j1"
    try:
        response = requests.get(url, timeout=10)
        response.raise_for_status()
        data = response.json()

        current = data.get("current_condition", [{}])[0]
        result = {
            "temperature_C": int(current.get("temp_C", "0")),
            "weather_desc": current.get("weatherDesc", [{}])[0].get("value", ""),
            "humidity": int(current.get("humidity", "0"))
        }
        return result

    except (requests.RequestException, ValueError, KeyError) as e:
        print(f"Failed to retrieve weather data: {e}")
        return None
```

## Why My Prompting Strategy Worked

By clearly listing specific improvements, including input validation, error handling, timeout, simplified data output, and documentation, the AI produced a more reliable, user-friendly function. This makes the function easier to understand and integrate into larger programs, improving overall code quality.
