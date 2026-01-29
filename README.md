# Creo

Hey there! Welcome to **Creo**, a custom-built HTTP client I wrote in Java. Think of it as a lightweight, open-source alternative to tools like Postman, but with a few unique twists (like built-in AI summaries).

I built this because I wanted to understand how HTTP clients work under the hood—managing connections, handling headers, and persisting data locally. It's a fully functional desktop application wrapped in a Swing GUI.

## What can it do?

*   **Send Requests**: Supports the standard method set: `GET`, `POST`, `PUT`, `DELETE`.
*   **Persistent History**: Unlike some CLI tools that forget everything when you close the terminal, Creo saves every single request and response to a local SQLite database (`oop.db`). You can browse your history anytime.
*   **AI-Powered Insights**: This is the cool part. If you get a massive JSON response and don't want to parse it manually, Creo can use the Groq API to generate a concise summary of the data for you.
*   **Clean UI**: A straightforward interface with tabs for Headers, Body, and Response views.

## Getting Started

### Prerequisites

You'll need a standard Java setup:
*   **Java JDK 11+** (I'm using newer features, so 21 is ideal, but it should work on modern LTS versions).
*   **Just** (Optional, but makes running commands easier).

### Setup

1.  **Compiling**:
    I've included a `Justfile` to make this easy.
    ```bash
    just build
    ```
    *If you don't have `just`, you can run:*
    `javac -d out/production/Creo -cp "lib/*" *.java`

### Running the App

To launch the main GUI:
```bash
just run
```
*(Or manually: `java -cp "out/production/Creo:lib/*" SimpleHTTPClientUI`)*

### Enabling AI Summaries (Optional)

If you want the AI summary feature to work, you need a Groq API key.
1.  Get a key from [Groq Console](https://console.groq.com).
2.  Set it as an environment variable before running the app:

**Linux/Mac:**
```bash
export GROQ_API_KEY="your_actual_api_key_here"
just run
```

**Windows (PowerShell):**
```powershell
$env:GROQ_API_KEY="your_actual_api_key_here"
just run
```

## How it Works

The project follows a layered architecture to keep things tidy:
*   **UI Layer**: `SimpleHTTPClientUI.java` handles the Swing components using a SplitPane layout (History on the left, Request/Response on the right).
*   **Service Layer**: `PostmanBackendService` acts as the brain, coordinating between the UI, the HTTP client, and the database.
*   **Data Layer**: `RequestsDAO` and `ResponsesDAO` handle all SQLite operations. We use a relational model where every Response is linked to its parent Request.

## Libraries Used

I tried to keep dependencies minimal:
*   **Google Gson**: For handling JSON.
*   **SQLite JDBC**: For the local database.
*   **CommonMark**: To render the AI's Markdown responses as HTML in the UI.
*   **FlatLaf**: To make Swing look a bit more modern.

Enjoy testing your APIs!
