# WeatherHub – iOS App

WeatherHub is an iOS weather application built in SwiftUI as part of my coursework at Florida Atlantic University.  
It integrates the Tomorrow.io Weather API to display current conditions and 5-day forecasts, using async/await for networking and JSON parsing.  

**Key Features:**
- SwiftUI interface with custom components
- Async/await networking for API calls
- 5-day forecast with data persistence
- Dynamic UI updates and clean design

⚡ Built as my final project for FAU’s Mobile App Development course.

# WeatherHub

## Table of Contents

1. [Overview](#Overview)
2. [Product Spec](#Product-Spec)
3. [Wireframes](#Wireframes)
4. [Schema](#Schema)

## Overview

### Description

WeatherHub is a weather application that provides users with real-time weather updates, detailed forecasts, and historical weather data based on their location or a specified area. It uses the Tomorrow.io Weather API to deliver accurate and hyper-local weather information through an intuitive and user-friendly interface.

### App Evaluation

- **Category:** Weather
- **Mobile:** Yes, optimized for mobile use.
- **Story:** Empowers users to stay informed about the weather conditions in their area or any location worldwide.
- **Market:** Targeted toward anyone needing accurate weather information, including commuters, travelers, and outdoor enthusiasts.
- **Habit:** Daily use for checking real-time and forecasted weather conditions.
- **Scope:** Focused on weather data, with room for additional features like historical weather or severe weather alerts.

## Product Spec

### 1. User Stories (Required and Optional)

**Required Must-have Stories**
- User can view real-time weather for their current location.
- User can see a 5-day weather forecast.
- User can search for weather in a specific city.
- User can toggle between Celsius and Fahrenheit.

**Optional Nice-to-have Stories**
- User can view historical weather data for a selected date.
- User receives notifications for severe weather alerts.
- User can enable dark mode for the interface.

## Milestone 4 Sprint Gif 
![Screen Recording 2024-12-06 at 10 14 40 PM](https://github.com/user-attachments/assets/f4a0cda1-2033-43e8-b2c3-ef646e304130)

## Milestone 5 Sprint Planning
![Screen Recording 2024-12-10 at 9 01 29 PM](https://github.com/user-attachments/assets/0cbe970b-a411-4cb7-b8af-ccdae6ec5b0e)

## Final Video Demo
![Weatherhubdemo](https://github.com/user-attachments/assets/c4db0015-27ed-46cd-aafc-3148501c29fb)


### 2. Screen Archetypes

- [x] **Home Screen**
  - User can view real-time weather information for their current location.
  - Displays temperature, weather conditions, and additional details (e.g., wind speed, humidity).
- [x] **Forecast Screen**
  - User can view a 5-day weather forecast with daily summaries.
- [x] **Map view**
  - User can view a map with digital radar overlay.
- [x] **Settings Screen**
  - User can toggle between Celsius and Fahrenheit and enable/disable notifications.

### 3. Navigation

**Tab Navigation** (Tab to Screen)
- [x] Home → Displays real-time weather.
- [x] Forecast → Shows 5-day weather forecasts.
- [x] Map view → Can view a map with digital radar overlay.
- [x] Settings → Enables toggling preferences like units.

**Flow Navigation** (Screen to Screen)
- [x] **Home** 
  - Leads to **Forecast**, and **Settings**.
- [ ] **Map View** 
  - Leads back to **Home** when selecting the correct tab.
- [ ] **Settings** 
  - Leads back to **Home** after saving preferences.

## Wireframes

![Wireframe1](https://github.com/user-attachments/assets/d4df85b8-5500-4922-91e5-87f68d2315c8)


## Schema

### Models

**Weather Model**
| Property      | Type      | Description                                    |
|---------------|-----------|------------------------------------------------|
| location      | String    | Name of the location (e.g., city name)         |
| temperature   | Float     | Current temperature of the location            |
| condition     | String    | Current weather condition (e.g., "Cloudy")     |
| forecast      | [Forecast]| Array of daily forecast data                   |

**Forecast Model**
| Property      | Type      | Description                                    |
|---------------|-----------|------------------------------------------------|
| date          | String    | Date for the forecasted weather                |
| temperature   | Float     | Forecasted temperature for the day             |
| condition     | String    | Weather condition for the day (e.g., "Rainy")  |

### Networking

**List of Network Requests by Screen**

**Home Screen**
- `[GET] /weather/realtime?location={latitude,longitude}` 
  - Fetches real-time weather for the user's current location.

**Forecast Screen**
- `[GET] /weather/forecast?location={latitude,longitude}`
  - Fetches a 5-day weather forecast for the user's current location.

**Search Screen**
- `[GET] /weather/realtime?location={city_name}`
  - Fetches real-time weather for a searched city.

**Settings Screen**
- `[POST] /user/preferences`
  - Saves user preferences for temperature unit and notifications.

**Example Network Request**
```swift
let url = URL(string: "https://api.tomorrow.io/v4/weather/realtime?location=Boston&apikey=YOUR_API_KEY")!
URLSession.shared.dataTask(with: url) { data, response, error in
    if let data = data {
        do {
            let weatherData = try JSONDecoder().decode(Weather.self, from: data)
            print(weatherData)
        } catch {
            print("Error decoding: \(error)")
        }
    }
}.resume()
```
