Zabbix Assistant
Zabbix Assistant is an AI-powered chatbot designed to interact with a Zabbix server, providing users with real-time monitoring insights and management capabilities. It leverages the LangGraph framework to handle Zabbix API calls dynamically and ensures smooth interactions without hardcoded data.

Project Structure

zabbix_assistant/
│── main.py                  # Entry point of the application
│── .env                     # Environment variables (Zabbix credentials, API keys, etc.)
│── requirements.txt         # List of required dependencies
│
│── logs/                    # Directory for storing logs
│   └── zabbix_assistant.log  # Log file for tracking errors and interactions
│
│── data/                    # Directory for storing data files
│   └── chat_history.csv      # Stores chat history for user interactions
│
│── config/                  # Configuration-related files
│   └── settings.py           # Configuration settings for the application
│
│── utils/                   # Utility functions and helper modules
│   ├── chat_history.py       # Functions for handling chat history (saving, retrieving)
│
│── modules/                 # Core application modules
│   ├── __init__.py           # Initializes the module as a package
│   ├── zabbix_tools.py       # Tools for interacting with Zabbix API (fetching hosts, metrics, etc.)
│   └── zabbix_assistant.py   # Main logic for processing user queries and invoking Zabbix API


Key Components
main.py: Entry point for the application.
.env: Stores environment variables like Zabbix API credentials.
requirements.txt: Lists all dependencies.
logs/: Stores log files for debugging.
data/: Stores chat history.
config/settings.py: Manages configuration settings.
utils/chat_history.py: Handles chat history storage and retrieval.
modules/zabbix_tools.py: Contains helper functions for Zabbix API interactions.
modules/zabbix_assistant.py: Core assistant logic and LangGraph integration.

Workflow Overview
+-------------------------+
|   Start / User Input    |
+-------------------------+
            |
            v
+-------------------------+
|  Initialize StateGraph  |  (Create a state machine to manage transitions)
|  & Memory Saver        |
+-------------------------+
            |
            v
+-------------------------+
|   Receive User Input    |  (Capture the user query, e.g., "Get me first 15 hosts")
+-------------------------+
            |
            v
+-------------------------+
|  Pass Input to Agent    |  (Pass the user query as HumanMessage to agent)
+-------------------------+
            |
            v
+-------------------------+
|  Agent Decides Action   |  (Agent chooses the appropriate tool based on input)
+-------------------------+
            |
            v
+-------------------------+
|  Tool Selection         |  (Invoke the selected tool from available tools)
|  e.g., `get_hosts`      |
+-------------------------+
            |
            v
+-------------------------+
|  Invoke Zabbix API      |  (Call Zabbix API to retrieve hosts or other info)
|  Fetch Data (e.g., hosts|
|  or items)              |
+-------------------------+
            |
            v
+-------------------------+
|  Process API Response   |  (Parse and format the response from Zabbix)
|  (Error Handling)       |
+-------------------------+
            |
            v
+-------------------------+
|  Generate AI Response   |  (AI generates response using Groq model)
|  (Based on API Data)    |
+-------------------------+
            |
            v
+-------------------------+
|  Send Response Back     |  (Send the generated response back to user as AIMessage)
+-------------------------+
            |
            v
+-------------------------+
|   Log Interaction       |  (Log the interaction for debugging and monitoring)
+-------------------------+
            |
            v
+-------------------------+
|   Repeat or Exit        |  (Loop to capture further input or exit on command)
+-------------------------+
Features
Chat-Based Zabbix Management: Query Zabbix for hosts, triggers, and issues using natural language.
Dynamic API Calls: Automatically selects the appropriate Zabbix API endpoint.
State Management with LangGraph: Handles complex interactions seamlessly.
Persistent Chat History: Saves conversations for later reference.
Logging & Debugging: Tracks interactions and errors for troubleshooting.

Setup Instructions

Clone the repository:
   git clone https://github.com/your-repo/zabbix_assistant.git
   cd zabbix_assistant

Install dependencies:
   pip install -r requirements.txt

Configure environment variables in .env:
   ZABBIX_API_URL=http://zabbix_server/zabbix/api_jsonrpc.php
   ZABBIX_USER=
   ZABBIX_PASSWORD=
   OPENAI_API_KEY=

Run the assistant:
   python main.py

Future Enhancements
- Implement a web-based UI with Streamlit.
- Add role-based authentication for Zabbix actions.
- Expand AI capabilities with advanced NLP models.
