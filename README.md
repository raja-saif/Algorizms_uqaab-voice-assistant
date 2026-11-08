# Uqaab Voice Assistant

A voice-enabled prototype driver assistant for the **Uqaab** freight-matching platform. A driver speaks a command, the app turns it into text, works out what the driver wants with regex patterns, and answers both aloud and in a Tkinter chat window.

## ✨ Features
- 🎤 **Speech-to-text** with the `SpeechRecognition` library and the Google Speech Recognition API
- 🧠 **Regex-based intent parsing** that also picks out details such as city names
- 🔊 **Text-to-speech** replies with `pyttsx3` (speech rate set to 150)
- 💬 **Tkinter GUI** in a dark theme, with a chat log, a status label ("Listening..." / "Ready"), and a **Speak** button
- 🧵 **Multithreading:** listening runs on a background thread so the GUI stays responsive
- 🚚 **Simulated backend:** in-memory driver data (current job and next job) stands in for the real platform

## 🗣 Supported voice commands
| Intent | Example command | Response |
|---|---|---|
| `update_route` | "Update my route to Lahore" | Updates the current job's destination and replies with a randomly chosen ETA (1–5 hours) |
| `next_job` | "What's my next job?" | Gives the next job's origin, destination, cargo, and pickup time |
| `next_delivery` | "When is my next delivery?" | Gives the current delivery's destination and due time |
| `cancel_job` | "Cancel my job" | Cancels the current job (for example JOB-78912) |
| `confirm_dropoff` | "Confirm drop-off in Lahore" | Confirms the drop-off and says payment will be processed |

If a command matches none of these, the assistant replies with a fallback message.

## 🛠 Tech stack
- Python 3.10+ (recommended)
- Tkinter / ttk (GUI)
- SpeechRecognition (Google Speech Recognition API)
- PyAudio (microphone input)
- pyttsx3 (offline text-to-speech)
- Standard library: `re`, `threading`, `datetime`, `random`

## ⚙️ How it works
1. The driver clicks **🎤 Speak**, and a background thread starts listening on the microphone, after first adjusting for ambient noise.
2. Google Speech Recognition transcribes the audio to text.
3. The lowercased text is checked against the regex patterns to find the intent and any city name.
4. The matching handler updates or reads the in-memory `driver_data` and builds a reply.
5. The reply appears in the chat window and is spoken aloud with `pyttsx3`.

## 📁 Project structure
```
Algorizms_uqaab-voice-assistant/
├── main.py                   # Assistant logic (UqaabVoiceAssistant) and GUI (UqaabGUI)
├── readme_Instructions.docx  # Setup notes, intents, and working overview
└── demo.mp4                  # Demo video
```

## 🚀 Setup & run
```bash
git clone https://github.com/raja-saif/Algorizms_uqaab-voice-assistant.git
cd Algorizms_uqaab-voice-assistant
pip install SpeechRecognition pyttsx3 pyaudio
python main.py
```
You need a working microphone and an internet connection, because speech recognition goes through Google's API. Tkinter ships with most Python installations.

## 🎬 Demo
See [`demo.mp4`](demo.mp4) in this repository.

---
**Author:** Raja Saif Ali — [GitHub](https://github.com/raja-saif) · [LinkedIn](https://www.linkedin.com/in/raja-saif-01702329a/)
