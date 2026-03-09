# Weather AI Agent - Complete Guide

## What Is This Program?

This is an **AI-powered weather assistant** that helps you get weather forecasts for any location. Think of it as a smart helper that:
1. **Listens** to your location request (like "Seattle" or "New York")
2. **Thinks** about what weather data you need using AI (Claude)
3. **Acts** by fetching real weather data from the National Weather Service
4. **Understands** the complex weather data and converts it into simple, easy-to-read information

It's called an "agentic" system because it behaves like an intelligent agent that can plan, execute tasks, and process information - similar to how a human assistant would help you.

## Two Versions Available

This project includes **TWO different versions** of the same weather agent:

### 1. **weather_agent_cli.py** - Command Line Version
**What it is:** A text-based program that runs in your terminal/command prompt

**Best for:**
- People who like simple, straightforward programs
- Running on servers or computers without a graphical interface
- Quick weather checks without opening a browser
- Learning how the agent works step-by-step

**How to run it:**
```bash
python weather_agent_cli.py
```

### 2. **weather_agent_web.py** - Web Interface Version
**What it is:** A beautiful, interactive web application with buttons, colors, and visual displays

**Best for:**
- People who prefer visual interfaces
- Seeing the agent's progress in real-time with colorful boxes
- Exploring the data with expandable sections
- Sharing with others who might not be comfortable with command line

**How to run it:**
```bash
streamlit run weather_agent_web.py
```

**Both versions do the exact same thing** - they just present the information differently! The CLI version is like reading a book, while the web version is like watching a movie of the same story.

---

## How Does It Work? (The Big Picture)

Imagine asking a smart assistant: "What's the weather in Seattle?"

Here's what happens behind the scenes:

```
You type: "Seattle"
    ↓
AI thinks: "I need coordinates for Seattle: 47.6062, -122.3321"
    ↓
Program fetches: Location data from weather service
    ↓
Program fetches: Detailed weather forecast
    ↓
AI processes: Raw weather data into simple summary
    ↓
You see: Easy-to-read weather forecast!
```

---

## Key Differences Between the Two Versions

| Feature | CLI Version | Web Version |
|---------|-------------|-------------|
| **Interface** | Plain text in terminal | Colorful web page with buttons |
| **Progress Display** | Text messages | Colored boxes (green for success, red for errors) |
| **Data Viewing** | Shows everything | Collapsible sections you can expand/hide |
| **Running Multiple Queries** | Type new location after each result | Click "Clear Results" button and enter new location |
| **Visual Appeal** | Simple and clean | Beautiful with styled boxes and layouts |
| **Learning Curve** | Need to know how to use terminal | Just click buttons like any website |
| **Setup Required** | Just Python | Needs Streamlit library installed |

**Core Functions:** Both versions use the exact same 5 core functions to do the work:
1. `call_claude_sonnet()` - Talk to AI
2. `execute_curl_command()` - Fetch data from internet
3. `generate_weather_api_calls()` - Generate API URLs
4. `get_forecast_url_from_points_response()` - Extract forecast URL
5. `process_weather_response()` - Convert data to readable summary

**Main Difference:** The 6th function is different:
- CLI uses: `run_weather_agent()` - Simple text-based loop
- Web uses: Streamlit code - Creates the visual interface

---

## Web Version Special Features

The `weather_agent_web.py` file includes additional features that make it more interactive:

### 1. **Custom Styling**
The web version has custom CSS (styling code) that creates:
- **Colored boxes** for different types of information
  - Green boxes for successful steps
  - Red boxes for errors
  - Blue boxes for informational messages
- **Rounded corners** and nice spacing
- **Professional fonts** and colors

### 2. **Sidebar Information**
A side panel that shows:
- What "Agentic AI" means
- The architecture diagram
- How the agent works

**Think of it like:** A helpful guide standing next to you explaining everything

### 3. **Expandable Sections**
You can click to show or hide:
- Raw API responses (the technical data)
- Details about each step

**Think of it like:** Drawer organizers - you can open them to see more, or close them to keep things tidy

### 4. **Interactive Buttons**
- "Get Weather Forecast" button - Starts the process
- "Clear Results" button - Clears the screen for a new search

**Think of it like:** Remote control buttons for your TV

### 5. **Real-time Progress**
As the agent works, you can see:
- Which step is currently running (with a spinner animation)
- Checkmarks for completed steps
- The workflow status on the side

**Think of it like:** A progress bar when you're downloading a file, but for each step

### 6. **Example Suggestions**
The web version shows helpful examples at the bottom:
- "Seattle" - Test a major city
- "90210" - Test a ZIP code
- "Largest City in California" - Test AI understanding

**Think of it like:** A menu at a restaurant showing you popular dishes to try

### 7. **Visual Layout**
The screen is divided into sections:
- **Main area**: Shows all the steps and results
- **Sidebar**: Shows information about the agent
- **Top**: Input box and buttons
- **Bottom**: Examples and tips

**Think of it like:** A well-organized newspaper with different sections for different content

---

## The Functions Explained (In Simple Terms)

**Note:** The following functions are used in BOTH versions (CLI and Web) and work exactly the same way.

### 1. **call_claude_sonnet(prompt)**
**What it does:** This is the "brain" of the agent - it talks to Claude AI.

**Think of it like:** Asking a very smart friend a question and getting an answer.

**How it works:**
- You give it a question or instruction (called a "prompt")
- It sends that question to Claude AI through Amazon's cloud service (AWS Bedrock)
- Claude thinks about it and sends back an answer
- The function returns the answer to you

**Example:**
```
Question: "What are the coordinates for Seattle?"
Answer: "Seattle is at 47.6062 latitude, -122.3321 longitude"
```

**Parameters:**
- `prompt`: The question or instruction you want to ask Claude (text)

**Returns:**
- Two things:
  - Success status (True if it worked, False if there was an error)
  - The answer from Claude (text)

---

### 2. **execute_curl_command(url)**
**What it does:** Fetches data from the internet using a specific web address (URL).

**Think of it like:** Opening a webpage and copying all the text from it.

**How it works:**
- You give it a web address (URL)
- It uses a tool called "curl" to visit that address
- It downloads whatever information is at that address
- It gives you back that information

**Example:**
```
URL: https://api.weather.gov/points/47.6062,-122.3321
Result: Information about Seattle's location from the weather service
```

**Parameters:**
- `url`: The web address to fetch data from (text)

**Returns:**
- Two things:
  - Success status (True if it worked, False if there was an error)
  - The data from the website (text)

---

### 3. **generate_weather_api_calls(location)**
**What it does:** Uses AI to figure out the correct web address to get weather data for your location.

**Think of it like:** Asking your smart assistant, "Where do I need to go to find weather information for Seattle?" and they give you the exact address.

**How it works:**
- You tell it a location name (like "Seattle" or "New York")
- It asks Claude AI to figure out the latitude and longitude coordinates for that place
- Claude creates the correct weather service web address (URL) for those coordinates
- It gives you back that URL

**Example:**
```
Input: "Seattle"
AI thinks: "Seattle is at 47.6062, -122.3321"
Output: "https://api.weather.gov/points/47.6062,-122.3321"
```

**Parameters:**
- `location`: The place you want weather for (text) - can be a city, state, or description

**Returns:**
- Two things:
  - Success status (True if it worked, False if there was an error)
  - A list containing the weather service web address (URL)

---

### 4. **get_forecast_url_from_points_response(points_json)**
**What it does:** Extracts the forecast web address from location data.

**Think of it like:** You got directions to a building, and now you need to find the specific room number inside. This function finds that room number.

**How it works:**
- The weather service first gives you location information (the "building")
- Hidden inside that information is another web address for the actual forecast (the "room number")
- This function digs through the data to find that forecast address
- It gives you back that specific forecast URL

**Example:**
```
Input: Complex location data with many details
Output: "https://api.weather.gov/gridpoints/SEW/124,67/forecast"
```

**Parameters:**
- `points_json`: The raw location data from the weather service (text in JSON format)

**Returns:**
- Two things:
  - Success status (True if it worked, False if there was an error)
  - The forecast web address (URL)

---

### 5. **process_weather_response(raw_json, location)**
**What it does:** Converts complicated weather data into a simple, easy-to-read summary.

**Think of it like:** You receive a thick technical manual about tomorrow's weather, and your smart assistant reads it all and tells you: "It'll be sunny and 75 degrees - perfect for a picnic!"

**How it works:**
- The weather service gives you lots of technical data (temperatures, wind speeds, humidity, etc.)
- This function sends all that data to Claude AI
- Claude reads through everything and creates a friendly, easy-to-understand summary
- It gives you back that nice summary

**Example:**
```
Input: 5000 characters of technical weather data with numbers and codes
Output: "Seattle Weather Summary: Today will be partly cloudy with a high of 68°F.
Light rain expected tomorrow morning. Weekend looks sunny and warm!"
```

**Parameters:**
- `raw_json`: The raw technical weather data (text)
- `location`: The place name (text) - helps Claude create a more personalized summary

**Returns:**
- Two things:
  - Success status (True if it worked, False if there was an error)
  - The friendly weather summary (text)

---

### 6. **Main Program Function (Different in Each Version)**

The sixth function is different depending on which version you're using:

#### **CLI Version: run_weather_agent()**
**What it does:** This is the "conductor" that orchestrates everything - it runs the whole show in the terminal!

**Think of it like:** The director of a play who makes sure all the actors (functions) do their parts in the right order.

**How it works:**

**Step 1:** Greets you and asks what location you want weather for

**Step 2:** Takes your location and asks the AI to generate the right web address (calls `generate_weather_api_calls`)

**Step 3:** Fetches location data from that address (calls `execute_curl_command`)

**Step 4:** Extracts the forecast address from that data (calls `get_forecast_url_from_points_response`)

**Step 5:** Fetches the actual weather forecast (calls `execute_curl_command` again)

**Step 6:** Sends the forecast to AI to make it readable (calls `process_weather_response`)

**Step 7:** Shows you the final, easy-to-read weather summary

**Step 8:** Asks if you want weather for another location, or if you want to quit

**Parameters:** None - it handles everything by asking you questions

**Returns:** Nothing - it just displays information on your screen

#### **Web Version: Streamlit Interface Code**
**What it does:** Instead of one main function, the web version uses Streamlit commands to create the visual interface.

**Think of it like:** Instead of a play director, it's like a TV producer who creates the set, places cameras, adds graphics, and makes everything look beautiful on screen.

**How it works:**
- Uses `st.title()`, `st.button()`, `st.text_input()` to create visual elements
- Calls the same 5 core functions when you click the button
- Displays results in colored boxes with `st.markdown()`
- Shows loading animations with `st.spinner()`
- Creates sidebars, columns, and layouts automatically

**The main difference:** CLI shows plain text line by line, while Web creates a full interactive webpage.

**Both do the same work** - they just present it differently!

---

## The Complete Workflow (Step-by-Step)

Let's walk through a complete example of what happens when you ask for weather in Seattle:

```
┌─────────────────────────────────────────────────────────────┐
│ YOU TYPE: "Seattle"                                         │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│ STEP 1: AI Planning Phase                                   │
│ Function: generate_weather_api_calls("Seattle")             │
│ AI thinks: "Seattle is at 47.6062, -122.3321"              │
│ Result: https://api.weather.gov/points/47.6062,-122.3321    │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│ STEP 2: Points API Execution                                │
│ Function: execute_curl_command(points_url)                  │
│ Action: Fetch location data from weather service            │
│ Result: JSON data with grid information                     │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│ STEP 3: Extract Forecast URL                                │
│ Function: get_forecast_url_from_points_response()           │
│ Action: Find the forecast URL in the location data          │
│ Result: https://api.weather.gov/gridpoints/SEW/124,67/...   │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│ STEP 4: Forecast API Execution                              │
│ Function: execute_curl_command(forecast_url)                │
│ Action: Fetch actual weather forecast data                  │
│ Result: JSON data with temperatures, conditions, etc.       │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│ STEP 5: AI Analysis Phase                                   │
│ Function: process_weather_response()                        │
│ AI reads: All the technical weather data                    │
│ AI creates: Simple, friendly weather summary                │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│ STEP 6: Display Results                                     │
│ YOU SEE: Easy-to-read weather forecast for Seattle!         │
└─────────────────────────────────────────────────────────────┘
```

---

## Key Concepts for Non-Programmers

### What is JSON?
JSON is a way to organize data that computers can easily read. Think of it like a filing cabinet where information is stored in labeled folders. For example:
```json
{
  "city": "Seattle",
  "temperature": 68,
  "condition": "Partly Cloudy"
}
```

### What is an API?
API stands for "Application Programming Interface." Think of it like a waiter at a restaurant:
- You (the customer) tell the waiter what you want
- The waiter takes your order to the kitchen
- The kitchen prepares your food
- The waiter brings it back to you

In our case:
- Our program is the customer
- The weather service API is the waiter
- The weather database is the kitchen

### What is a URL?
A URL is a web address - like a street address for information on the internet.
Example: `https://api.weather.gov/points/47.6062,-122.3321`

### What does "Agentic" mean?
An "agentic system" is a program that can:
1. **Plan** - Figure out what needs to be done
2. **Act** - Do things on its own
3. **Learn/Adapt** - Use feedback to improve results

Our weather agent does all three:
- **Plans:** Figures out what coordinates to use
- **Acts:** Fetches data from the internet
- **Adapts:** Processes raw data into useful information

---

## What Makes This "AI-Powered"?

Traditional weather programs have fixed instructions:
```
If user types "Seattle" → Always use coordinates 47.6062,-122.3321
If user types "New York" → Always use coordinates 40.7128,-74.0060
```

Our AI-powered agent is smarter:
```
User types: "The largest city in Washington state"
AI understands: "That's Seattle" → Uses coordinates 47.6062,-122.3321

User types: "Where the Space Needle is"
AI understands: "That's also Seattle!" → Uses coordinates 47.6062,-122.3321
```

The AI can understand natural language and descriptions, not just exact city names!

---

## Technical Details (For Those Curious)

### Libraries Used (Both Versions):
- **boto3**: Connects to Amazon Web Services (AWS) to access Claude AI
- **json**: Reads and processes JSON data
- **subprocess**: Runs system commands (like curl)
- **time**: Handles timing operations
- **datetime**: Works with dates and times

### Additional Libraries (Web Version Only):
- **streamlit**: Creates the web interface with buttons, boxes, and layouts
- **PIL (Pillow)**: Handles image processing (for icons and graphics)
- **os**: Manages file system operations

**What is Streamlit?**
Streamlit is a Python library that makes it super easy to turn Python scripts into beautiful web applications. Instead of writing complex web code (HTML, CSS, JavaScript), you just write Python commands like `st.button()` and Streamlit automatically creates a nice-looking button on a webpage!

**Think of it like:** A magic translator that converts simple Python instructions into fancy websites.

### AI Model:
- **Claude 4.5 Sonnet**: A powerful AI model from Anthropic
- **Model ID**: `us.anthropic.claude-sonnet-4-5-20250929-v1:0`
- **Temperature**: Set to 0.7 (balanced between creative and focused)
- **Max Tokens**: 2000 (roughly 1500 words maximum response)

### Weather Service:
- **Provider**: National Weather Service (NWS)
- **API**: Free, public weather data for US locations
- **Format**: JSON (structured data)
- **Endpoints Used**:
  - Points API: `https://api.weather.gov/points/{lat},{lon}`
  - Forecast API: `https://api.weather.gov/gridpoints/{office}/{x},{y}/forecast`

---

## Common Questions

**Q: Which version should I use - CLI or Web?**
A:
- Use **CLI version** if you want a simple, fast, no-frills experience
- Use **Web version** if you want a visual, interactive experience with colors and buttons
- Both do the exact same thing, just presented differently!

**Q: Does this work for any location?**
A: It works best for US locations since it uses the National Weather Service. For international locations, the API calls may fail.

**Q: Do I need internet connection?**
A: Yes! The program needs to connect to both Claude AI (for thinking) and the weather service (for data).

**Q: How accurate is the weather data?**
A: Very accurate! It comes directly from the National Weather Service, the same source used by many weather apps.

**Q: Can I ask for weather in different ways?**
A: Yes! You can say "Seattle", "Seattle, WA", "98101" (zip code), or even "largest city in Washington state" - the AI understands them all.

**Q: What if I type an invalid location?**
A: The program will either show an error message or the AI might make a best guess. The weather service will return an error if the coordinates are invalid.

**Q: Do I need to install anything special?**
A:
- For **CLI version**: Just Python and the required libraries (boto3, json, subprocess)
- For **Web version**: You also need to install Streamlit (`pip install streamlit`)

**Q: Can both versions run at the same time?**
A: Yes! They're completely independent. You can have one running in the terminal and one in your web browser simultaneously.

**Q: Which version is better for learning how it works?**
A: The **CLI version** is better for learning because it shows you each step clearly in order. The **Web version** is better for demonstrating to others or for regular use because it looks more professional.

---

## Summary

This weather agent demonstrates how AI can be used to create intelligent systems that:
1. **Understand** natural language (your location descriptions)
2. **Plan** the right actions (figuring out coordinates and API calls)
3. **Execute** tasks (fetching data from the internet)
4. **Process** information (turning technical data into friendly summaries)

The core functions work together like a team:
- `call_claude_sonnet()` → The brain (thinks and reasons)
- `execute_curl_command()` → The hands (fetches data)
- `generate_weather_api_calls()` → The planner (creates strategy)
- `get_forecast_url_from_points_response()` → The navigator (finds paths)
- `process_weather_response()` → The translator (makes data understandable)
- Main function → The conductor (orchestrates everything)

Together, they create a powerful AI assistant that makes getting weather forecasts easy and conversational!

**Whether you use the CLI or Web version, you're experiencing the same intelligent agentic AI system - just through different interfaces!**

---

## Files Explained

This README explains both Python files in this project:

### 1. **weather_agent_cli.py** (Command Line Version)
- Text-based interface
- Runs in terminal/command prompt
- Simple and straightforward
- 287 lines of code
- Uses: `run_weather_agent()` as main function

### 2. **weather_agent_web.py** (Web Interface Version)
- Visual interface with colors and buttons
- Runs in web browser
- Beautiful and interactive
- 406 lines of code
- Uses: Streamlit commands for interface creation

**Both files share the same 5 core functions** and differ only in how they present information to you!

---

## Quick Start Guide

### To Run the CLI Version:
```bash
python weather_agent_cli.py
```
Then type a location and press Enter!

### To Run the Web Version:
```bash
streamlit run weather_agent_web.py
```
Your browser will open automatically. Enter a location and click the button!

---

Created: 2026-03-09
Updated: 2026-03-09 (Added web version documentation)
