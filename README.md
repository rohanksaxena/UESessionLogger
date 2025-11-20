# Session Logger (v2.0.1)

A lightweight **Universal runtime logger** for Unreal Blueprints.
Log **structs**, **arrays**, **maps**, and **primitive values** directly from Blueprints. No C++ setup required.

---

## ✨ Highlights
- Works in **Editor**, **PIE**, **Standalone**, and **Packaged** builds  
- Automatically creates per-session `.jsonl` files under `Saved/Logs`  
- Logs are **structured JSON**, easy to parse or feed into analytics tools  
- Optional **Flatten Mode** converts nested data into dotted key/value pairs 
- Color-coded console echo for INFO, WARNING, and ERROR levels
- Custom log levels supported with your own labels
- Automatic file rotation and old log cleanup
- Settings panel under Project Settings → Plugins → Session Logger
- Blueprint-first API: drop-in nodes, no coding needed

[Download the demo project here](https://drive.google.com/file/d/1THopd2BDwNcgILBJnTCoOgJ2pAlSu-Vi/view?usp=sharing) 
---

## 🚀 Quick Start

1. **Install the Plugin**
   - Install the plugin from Epic's Fab marketplace.
   - In Unreal → *Edit → Plugins* → Enable **Session Logger** → Restart.

2. **Initialize the Logger**
   - In your Level Blueprint or GameInstance:
     ```blueprint
     Init Logger (Self)
     Log Message (Level: INFO, Message: "Logger started", Phase: "Startup")
     ```

3. **Run and Check Logs**
   - Launch PIE or and run a packaged game.
   - The default log file is created at:
     ```
     <ProjectRoot>/Saved/Logs/<ProjectName>_sessions.jsonl
     ```

4. **Example Log Line**
   ```json
   {
	  "project": "SessionLogger_Demo",
	  "ts": "2025-11-05T14:14:15.052Z",
	  "session": "C3C6C84245C7E34851D124AF057B0234",
	  "source": "unreal|L_Demo",
	  "level": "ERROR",
	  "message": "Something went wrong!",
	  "phase": "Startup"
	}
   ```


## 🧩 Blueprint Nodes Overview

| Node | Purpose |
|------|----------|
| **Log Message** | Logs a textual message with a Level (INFO, WARNING, ERROR, or CUSTOM). Custom lets you define your own label. |
| **Log Value** | Logs a single primitive value (Int, Float, Bool, String, Name, Text, Byte, Int64). |
| **Log Struct** | Serializes a struct into JSON and logs it. |
| **Log Array** | Serializes an array of primitives or structs into JSON. |
| **Log Map** | Logs a map of key/value pairs as JSON. |
| **Log Event JSON** | Logs a pre-built JSON object, array, or scalar. |
| **Init Logger** | Initializes the Session Logger subsystem for this session. |
| **Get Session Id** | Returns the current Session ID for the run. |
| **Is Logger Ready** | Returns true if the subsystem is initialized and ready to log. |

---

## ⚙️ Project Settings

Location: Edit → Project Settings → Plugins → Session Logger

| Setting | Description |
|------|----------|
| **Log Root Directory** | Base folder where log files are saved (relative or absolute). |
| **Log File Name** | File name for the active session log. Defaults to {ProjectName}_sessions.jsonl. |
| **Max File Size (MB)** | File rotation threshold. When reached, the file is renamed and a new one starts. |
| **Retention Days** | Old rotated log files older than this are deleted automatically. |
| **Cleanup Interval (seconds)** | Periodic cleanup interval. Set to 0 to disable. |
| **Log Event JSON** | Logs a pre-built JSON object, array, or scalar. |
| **Rotate on Startup** | If enabled, rotates an oversized log file at startup. |
| **Echo to Console** | When enabled, log lines are printed to the Unreal Output Log. Useful for debugging. |
| **Color-coded Output** |INFO = white, WARNING = yellow, ERROR = red (Only applies to the Unreal Output Log). |

---

## 🧠 How It Works
- SessionLoggerSubsystem (a GameInstanceSubsystem) manages all file I/O, session state, and rotation logic.
- Each run generates a **new SessionId** and appends to the JSON file. If no file is present, a new one is created. If the old one exceeds the "Max File Size", it is rotated and a new file is created. 
- Every log line includes:  
  `project`, `ts`, `session`, `source`, and either `level/message` or `event/data`.
- Rotation: When a file exceeds Max File Size (MB), it’s renamed with a timestamp and a new file starts automatically.
- Retention: Older logs are automatically deleted after Retention Days.

---

## 🧰 Example Log Variants

| Type | Example JSON |
|------|----------|
| **Message** | {"level":"INFO","message":"Game started","phase":"Startup"} |
| **Custom Label** | {"level":"NETWORKFAIL","message":"Connection lost"} |
| **Struct Log** | {"event":"PlayerStats","data":{"hp":100,"score":420}} |
| **Value Log** | {"event":"Speed","data":{"value":3.5}} |

---

## 🧾 Version 2.0.1 Highlights

- Enum-based Log Message node with color-coded console output
- Added Custom Label for user-defined log levels
- New Project Settings panel (directory, file name, rotation, cleanup)
- File rotation & retention system added
- LogEventJson_Object supports direct JsonObject payloads
- Backward-compatible JSON format for analytics tools
- Now compatible with Unreal Engine versions 5.4-5.7

---
AI Disclosure: This plugin’s code and documentation were authored and reviewed by a human. No AI-generated content or assets are included.
