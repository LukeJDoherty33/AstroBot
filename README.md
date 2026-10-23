# 🚀 Space Bot API Investigation Sheet

**Total Marks: 40**  
**TASK 1: Collect Required API Documentation**

This investigation sheet helps you gather key technical information from the three APIs required for the Space Bot project: **Webex Messaging API**, **ISS Current Location API**, **Weather API** and a **Geocoding API** , plus the Python time module. Also furhter investigate the application of Web Architecture and MVC design pattern in development of the Bot

---

##  Webex Messaging API (4 marks)

| Criteria | Details |
|---------|---------|
| API Base URL | `https://webexapis.com/v1` |
| Authentication Method | `Bearer  Token` |
| Endpoint to list rooms | `GET /rooms` |
| Endpoint to get messages | `GET /messages` |
| Endpoint to send message | `POST /messages` |
| Required headers | `Authorization: Bearer YOUR_ACCESS_TOKEN | Content-Type: application/json` |
| Sample full GET or POST request | `GET https://webexapis.com/v1/messages?roomId=YOUR_ROOM_ID` |

---

##  ISS Current Location API (2 marks)

| Criteria | Details |
|---------|---------|
| API Base URL | `https://api.open-notify.org` |
| Endpoint for current ISS location | `/iss-now.json` |
| Sample response format (example JSON) |  
```
```
|{
  "message": "success",
  "timestamp": 1729504800,
  "iss_position": {
    "latitude": "40.7128",
    "longitude": "-74.0060"
  }
  }
---

##  Geocoding API (4 marks)

| Criteria | Details |
|---------|---------|
| Provider used (Choose one) | **LocationIQ / Mapbox/ OpenWeatherMap other -provide detail** |
| API Base URL | `https://api.openweathermap.org/geo/1.0` |
| Endpoint for geocoding | `/direct` |
| Endpoint for reverse geocoding | `/reverse` |
| Authentication method | `API KEY` |
| Required query parameters | `Geocoding: q, appid; Reverse geocoding: lat, lon, appid. Optional: limit` |
| Sample request with latitude/longitude | `GET https://api.openweathermap.org/geo/1.0/reverse?lat=51.5074&lon=-0.1278&limit=1&appid=YOUR_API_KEY` |
| Sample JSON response (formatted example) |  
```
```
|{
    "name": "London",
    "local_names": {
      "en": "London"
    },
    "lat": 51.5074,
    "lon": -0.1278,
    "country": "GB"
  }
---

##  Weather API (3 marks)

| Criteria | Details |
|---------|---------|
| API Provider (Choose one) | **OpenWeather, OpenWeatherMap (or other – provide details)** |
| API Base URL | `https://api.openweathermap.org/data/2.5` |
| Endpoint for current weather | `/weather` |
| Authentication method | `API KEY` |
| Required query parameters | `q(city name), appid (API key), Optional:units=metric` |
| Sample JSON response (formatted example) |  
```
```
|{
  "name": "London",
  "main": {
    "temp": 15.5,
    "humidity": 75,
    "feels_like": 14.2
  },
  "weather": [
    {
      "main": "Clouds",
      "description": "scattered clouds"
    }
  ],
  "wind": {
    "speed": 4.2
  }
---

##  Epoch to Human Time Conversion (Python time module) (2 marks)

| Criteria | Details |
|---------|---------|
| Library used | `datetime` |
| Function used to convert epoch | `datetime.fromtimestamp()` |
| Sample code to convert timestamp |  
```  
```
|
| Output (human-readable time) | `2024-10-21 11:20:00 UTC` |

---

##  Extended Feature API ( 3 marks)

| Criteria | Details |
|---------|---------|
| API Provider | '_________' |
| API Base URL | `_______________________________` |
| Endpoint | `_______________________________` |
| Authentication method | `_______________________________` |
| Required query parameters | `_______________________________` |
| Sample JSON response (formatted example) |  
```

```
|

--- 

##  Evaluation – Web Architecture, MVC Design & Security 

In this section, evaluate how web technologies, architecture, and design patterns have been applied in your **AstroBot**. Your responses must relate directly to your implementation and include reflection on your design decisions.

---

###  Web Architecture – Client–Server Model (3 marks)

Explain how the client–server model applies to your AstroBot:

- Identify the **client**
the client is the python application, which runs using python idle and user interact with the bot by using certain commands through Webex
- Identify the **server(s)**
Webex API, OpenWeather API, Open Notify API
- Describe how data flows between:
  - User, AstroBot and APIs
when a user sends a command such as /weather london in Webex the astro bot uses request.get to retrieve data from the Webex API to which the bot sends a request to OpenWeather geocoding to find london lat and long, which uses those measurements to request weather information from the OpenWeather API. The data is return to the bot as a json, then uises request.post to send the information for the user to read

Include a **simple block diagram** to illustrate this interaction.

####  Security Considerations: (3 marks )
- Consider but not limiting to secure handling of API keys and tokens, API rate limiting, and Input validation (e.g., handling user commands safely), include examples from code where necessary to illustrate.
My bot requires Webex access token and OpenWeather API key to which i dont share the credentials so authorised access to the services are accessable.
---

###  RESTful API Usage in Your Application (3 marks )

Explain how REST APIs are used in your AstroBot: 

- Describe how HTTP methods (GET, POST) are used.
the GET method is used to request to retrieve information from a certain API. the post method is used so the bot can reply to the user.
- Explain how your bot interacts with APIs (Webex, Weather, ISS, Geocoding)
the bot uses GET and POST to gain infromation such as messages for Webex, weather information from OpenWeather API , current latitude and longitude from thje Open Notify API. 
- Describe how JSON responses are received and processed
the code data = response.json() converts the JSON response into a pyhton string

Note: Relate your explanation directly to your code for higher grade. 

#### Security Considerations: (2 marks)
- Check response status codes, Handling invalid or unexpected API responses, Avoiding excessive API calls
if response.status_code != 200:
    return "Unable to retrieve weather data." this line of code basically mean if the API displays a different number, the bot will display an error message.
if not location:
    return "City not found." if the coordinates are not correlated to a city the function returns none.
---

###  MVC Design Pattern in AstroBot (3 Marks)

Explain how the **Model–View–Controller (MVC)** pattern applies to your solution:
Provide a short example based on your implementation

| Component   | Description and Example (Relate to your Bot) |
|------------|----------------------------------|
| **Model**  | The Model handles retrieving and processing data. My Astro Bot uses, the get_weather(), get_city_coordinates() and get_iss_location() to retrieve information from APIs|
| **View**   | The View presents information to the user. my Astro Bot uses, the send_message() function to send information to the user through Webex |
| **Controller** | The Controller handles user commands. my Astro Bot uses, the main() function checks messages for commands such as /weather |

---

### 📝 Reflection and Evaluation ( 8 marks )

Reflect on your AstroBot (400 words):

- How effective is your bot in meeting the Astronomy Club’s needs?  
- What design decisions worked well?  
- What challenges did you face when integrating APIs?  
- What security risks did you identify and how were they handled?  
- How could your solution be improved in the future?  

---

 **Tip:** Link your answers directly to your code and examples for higher marks.
### Notes

- Use official documentation for accuracy (e.g. developer.webex.com, locationiq.com or Mapbox, open-notify.org or other ISS API).
- Be prepared to explain your findings to your instructor or demo how you retrieved them using tools like Postman, Curl, or Python scripts.

---

###  Total: /40
