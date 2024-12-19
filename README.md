# YouTubeLiveStreamChat
Google's API for reading YouTube live stream chat messages is very limited. It lasts only a few minutes. Other applications exist that can get this data without it but do so in JS. This is a template for C#. This repository provides a framework for integrating YouTube live chat functionality into your application. It leverages Google’s YouTube API, along with `Masterchat` for handling chat messages and `Edge.js` for extending functionality. Below is an explanation of the key components and how they fit together.

---

## Overview of Components

### 1. **Main Program**
   **File**: `MainProgram.cs`

   The `MainProgram` class serves as the entry point for initializing and running the chat integration. It:
   - Authenticates with YouTube using OAuth.
   - Retrieves the live chat ID for the specified YouTube channel or a backup URL.
   - Initializes the `ChatService` with a `ChatCallbacks` instance.

   **Key Methods:**
   - `RunChatIntegration`: Orchestrates the entire chat initialization process by authenticating, fetching live chat information, and setting up the chat service.

---

### 2. **Chat Service**
   **File**: `ChatService.cs`

   The `ChatService` class handles real-time communication with YouTube live chat. It:
   - Listens to live chat messages using the live chat ID.
   - Processes incoming chat messages by invoking the appropriate callbacks.

   **Dependencies:**
   - `Masterchat`: A lightweight library for fetching live YouTube chat messages.

   **Key Methods:**
   - `InitializeChat`: Sets up a connection to the YouTube live chat.
   - `ListenForMessages`: Continuously polls for new chat messages.

---

### 3. **Chat Callbacks**
   **File**: `ChatCallbacks.cs`

   This class defines the logic for handling received chat messages and errors. It:
   - Filters out duplicate messages.
   - Ignores messages received within a specific timeframe after the bot starts to avoid redundant processing.
   - Triggers an external event (`MessageReceived`) for further processing in the UI or other components.

   **Key Properties:**
   - `MessageReceived`: An event triggered for each new valid chat message.

   **Key Methods:**
   - `OnMessageReceived`: Parses and processes incoming messages.
   - `OnChatError`: Logs any errors encountered during message processing.

---

### 4. **YouTube Service Manager**
   **File**: `YouTubeServiceManager.cs`

   Manages interactions with YouTube’s API, specifically for:
   - Searching for the channel ID based on the channel name.
   - Fetching the live broadcast and chat information for the channel.
   - Extracting live chat IDs from backup URLs if no live broadcasts are found.

   **Key Methods:**
   - `GetLiveChatIdAsync`: Fetches the live chat ID or uses the backup URL.
   - `ExtractVideoIdFromUrl`: Extracts the video ID from a provided YouTube URL.

---

### 5. **Form1 (UI)**
   **File**: `Form1.cs`

   Provides a Windows Forms interface for interacting with the chat integration. It:
   - Displays live chat messages and tracked terms.
   - Allows users to add, reset, or delete tracked terms.
   - Updates the UI dynamically with rankings of tracked terms.

   **Key Features:**
   - Buttons for exporting/importing tracked terms.
   - Integration with `ChatCallbacks` to process and display live messages.
   - Logging system for displaying application and debug logs.

---

### 6. **Logger**
   **File**: `Logger.cs`

   Handles logging for the application. It:
   - Writes logs to both the console and a file (`app.log`).
   

   **Key Methods:**
   - `Log`: Writes a message to the console and appends it to the log file.

---

### 7. **Masterchat**
   **Source Attribution:**
   - Repository: [Masterchat GitHub](https://github.com/ytmdes/masterchat)

   `Masterchat` is a library that simplifies interactions with YouTube live chat. It provides:
   - Methods for fetching live chat messages efficiently.
   - Error handling for common API limitations and issues.

   **Usage:** This project uses `Masterchat` within the `ChatService` to retrieve and parse live chat messages.

---

### 8. **Edge.js**
   **Source Attribution:**
   - Repository: [Edge.js GitHub](https://github.com/agracio/edge-js)

   `Edge.js` allows seamless interoperability between C# and Node.js. This project uses it to:
   - Extend the chat integration with Node.js scripts.
   - Handle advanced features like message parsing and API interaction.

---

## Getting Started

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/yourusername/chat-integration-template.git
   ```

2. **Set Up Dependencies:**
   - Install the required NuGet packages:
     - `Google.Apis.YouTube.v3`
     - `Masterchat`
     - `Newtonsoft.Json`
   - Ensure you have Node.js installed for `Edge.js` compatibility.
   - YOUR PROJECT MUST BE .NET FRAMEWORK 4.6.2 FOR EDGE.JS TO WORK

3. **Authenticate with YouTube:**
   - Add your `ClientId` and `ClientSecret` to the `AuthService` class.
   - Run the application and authenticate using your YouTube account.

4. **Run the Application:**
   - Use Visual Studio to build and run the solution.
   - Enter the channel name and backup URL in the UI, then click "Update Settings" to start chat integration.

---

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

## Acknowledgments
Special thanks to the authors of [Masterchat](https://github.com/ytmdes/masterchat) and [Edge.js](https://github.com/agracio/edge-js) for providing invaluable tools that made this integration possible.

