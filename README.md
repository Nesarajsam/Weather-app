🌦 Weather App - Full Theory Explanation

1. **HTML Structure**
The HTML part builds the **skeleton** of the app:

- `<div class="card">`:  
  A container that holds everything (search bar, weather info, etc.).

- `<div class="search">`:  
  Contains:
  - An `<input>` field where users type the city name.
  - A `<button>` with a search icon to trigger the search.

- `<div class="error">`:  
  Hidden by default.  
  It shows an error message ("Invalid city name") if the city entered is not found.

- `<div class="weather">`:  
  Displays:
  - Weather icon (like rain, cloud, etc.)
  - Temperature (`<h1 class="temp">`)
  - City name (`<h2 class="city">`)
  - Two extra details:
    - Humidity
    - Wind speed

---
 2. **CSS (External `style.css`)**
(Not shown yet, but important.)

The CSS file is linked with:
```html
<link rel="stylesheet" href="style.css">
```
It is used to **style** the page — like background colors, font sizes, card shapes, and hiding/showing `.error` and `.weather` sections.

---

## 3. **JavaScript Logic**
This is the brain of the app.

- **API Setup**:
  ```javascript
  const apiKey = "your_API_key";
  const apiUrl = "https://api.openweathermap.org/data/2.5/weather?units=metric&q=";
  ```
  These connect to **OpenWeatherMap API** to get real-time weather data.

- **Elements Targeted**:
  ```javascript
  const searchBox = document.querySelector(".search input");
  const searchBtn = document.querySelector(".search button");
  const weatherIcon = document.querySelector(".weather-icon");
  ```
  Grabbing the HTML elements so JavaScript can control them.

- **Weather Checking Function**:
  ```javascript
  async function checkWeather(city) { ... }
  ```
  A function that:
  - Sends a request to the weather API for the entered city.
  - Waits for the response.
  - If the city is not found (404 error), it shows the error message.
  - If the city is found:
    - It updates the temperature, city name, humidity, and wind speed on the page.
    - It changes the weather icon based on the weather condition (Rain, Clouds, Clear, etc.)

- **Button Click Event**:
  ```javascript
  searchBtn.addEventListener("click", () => {
    checkWeather(searchBox.value);
  });
  ```
  When the user clicks the search button, the app calls the `checkWeather` function using the value typed in the input box.

---

## 4. **API Response Data**
When you ask the OpenWeather API for a city's weather, it sends you back **JSON data** like:

```json
{
  "name": "New York",
  "main": {
    "temp": 22.3,
    "humidity": 50
  },
  "wind": {
    "speed": 15
  },
  "weather": [
    { "main": "Rain" }
  ]
}
```

You then **extract** the important parts:
- `data.name` ➔ City Name
- `data.main.temp` ➔ Temperature
- `data.main.humidity` ➔ Humidity
- `data.wind.speed` ➔ Wind speed
- `data.weather[0].main` ➔ Weather condition (for image)

---

# 📚 Final Flow
1. User types a city name and clicks the search button.
2. JavaScript sends a request to OpenWeatherMap.
3. If city is valid ➔ shows temperature, city, humidity, wind, and correct weather icon.
4. If city is invalid ➔ shows "Invalid city name" error message.

---

# ⚡ Quick Improvements You Could Add
- Make it work when pressing **Enter** key also (not just button click).
- Add **loading spinner** while waiting for API.
- Add **background color changes** based on the weather.
- Improve **mobile responsiveness** with media queries.
