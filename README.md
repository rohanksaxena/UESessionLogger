# Session Logger (SL) for Unreal Engine

A lightweight **Blueprint-first JSONL logger** for Unreal Engine 5.  
Log **structs**, **arrays**, **maps**, and **primitive values** directly from Blueprints. No C++ setup required.

---

## ✨ Highlights
- Works in **Editor**, **PIE**, **Standalone**, and **Packaged** builds  
- Automatically creates per-session `.jsonl` files under `Saved/Logs`  
- Logs are **structured JSON**, easy to parse or feed into analytics tools  
- Optional **Flatten Mode** converts nested data into dotted key/value pairs  
- Blueprint-first API: drop-in nodes, no coding needed

---

## 🚀 Quick Start

1. **Install the Plugin**
   - Copy `SessionLogger/` into your project’s `Plugins/` folder.  
   - In Unreal → *Edit → Plugins* → Enable **Session Logger** → Restart.

2. **Initialize the Logger**
   - In your Level Blueprint or GameInstance:
     ```blueprint
     APP_InitLogger(Self)
     App Log Message ("INFO", "Logger started", "Startup")
     ```

3. **Run and Check Logs**
   - Launch PIE or a packaged build.
   - Open:
     ```
     <ProjectRoot>/Saved/Logs/<ProjectName>_sessions.jsonl
     ```

4. **Example Log Line**
   ```json
   {
     "project":"MyGame",
     "ts":"2025-10-04T23:25:55.166Z",
     "session":"A1B2C3D4E5F6",
     "source":"unreal|LevelName",
     "event":"Struct.Transform",
     "phase":"Startup",
     "data":{"location":{"x":8,"y":16,"z":24},"scale3D":{"x":1.5,"y":1,"z":0.5}}
   }
   ```


## 🧩 Blueprint Nodes Overview

| Node | Purpose |
|------|----------|
| **App Log Message** | Writes a simple breadcrumb (`Level`, `Message`, `Phase`). |
| **App Log Value** | Logs a primitive value (Int, Bool, String, Float, Name, Text, Byte, Int64). |
| **App Log Struct** | Serializes a struct into JSON and logs it. |
| **App Log Array** | Serializes an array into JSON and logs it. |
| **App Log Map** | Serializes a map into JSON and logs it. |
| **App Log Event JSON** | Sends a pre-built JSON object/array/scalar directly. |
| **APP Init Logger** | Ensures the subsystem is initialized before logging. |
| **APP Get Session Id** | Returns the current SessionId string. |
| **APP Is Logger Ready** | Returns true if the logger subsystem is initialized. |

---

## 🧠 How It Works
- A custom `GameInstanceSubsystem` (`AppSessionLogSubsystem`) handles initialization, file writing, and session tracking.
- Each run generates a **new SessionId** and creates/rotates a JSONL file.
- Every log line includes:  
  `project`, `ts`, `session`, `source`, and either `level/message` or `event/data`.

---

AI Disclosure: This plugin’s code and documentation were authored and reviewed by a human. No AI-generated content or assets are included.
