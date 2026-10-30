# VoiceCapsule V2.0.0 User Manual

**Lightweight · Offline-First · Privacy-Focused · Speech-to-Video-to-Text Tool**

> Say it when you think of it, and you have the text. When you don't want to type, just speak.

VoiceCapsule is a local speech recognition-based voice input and audio/video-to-text tool for Windows and Ubuntu Linux.

It converts speech from your computer microphone into text, and can also import audio or video files to generate transcripts, subtitles, and time-aligned text files.

VoiceCapsule prioritizes local execution and does not require a cloud speech service subscription. The Full version also integrates third-party API features, allowing you to choose whether to use online services.

---

## Download VoiceCapsule

Please go to the **Releases** page of the GitHub project and download according to your OS and needs.

| OS | Version | Download File |
|---|---|---|
| Windows | Full | `VoiceCapsule_V2_win.zip` |
| Windows | Free | `VoiceCapsule_V2_win_free.zip` |
| Ubuntu Linux | Full | `VoiceCapsule_V2_linux.zip` |
| Ubuntu Linux | Free | `VoiceCapsule_V2_linux_free.zip` |

For differences between Free and Full, please see "Free vs Full" at the end of this document.

---

## 1. What is VoiceCapsule?

VoiceCapsule is not just a voice input tool. It can also process speech in audio and video, converting it into text and subtitles.

### Core Features

- **Local Speech Recognition:** Runs locally using Faster-Whisper.
- **Auto Language Detection:** You are not limited to Chinese just because the UI is in Chinese.
- **Multiple Whisper Models:** small, medium, large-v3, large-v3-turbo.
- **Cross-App Text Input:** After recognition, text can be typed into any app that accepts text input.
- **Dictionary Correction:** Common errors and personal dictionary to fix common mistakes.
- **Audio/Video to Text:** Converts speech in media to text.
- **Multiple Output Formats:** TXT, SRT, LRC.
- **Offline-First:** General local recognition does not depend on paid cloud speech services.
- **Full Version API:** Users can configure supported third-party APIs.

## 2. What Can You Use VoiceCapsule For?

### Daily Voice Input
- Chat and messaging, Email, Word, Google Docs, Notion, LibreOffice, Browsers, Code editors, Note-taking apps

### Content Creation
- Novels and articles, Script writing, Social posts, Long-form dictation, Work logs, Personal notes

### Audio & Video Processing
- Interview transcripts, Meeting minutes, Lecture recording to text, Audio to text, Video to text, Subtitle creation, Lyric timeline creation, Audio/video speech translation to English

## 3. Microphone Voice Input

### How to Use
1. Place the text cursor in the target app.
2. Start recording with VoiceCapsule.
3. Default recording time is 10 seconds, adjustable in System Settings.
4. You can stop early during recording.
5. After recording, VoiceCapsule performs speech recognition.
6. After recognition, text is typed into the target app.

No need to hold down a button while speaking.

### What Files Does Recording Generate?
- **WAV:** Microphone recording file.
- **TXT:** Text file after recognition.

These are stored in the `audio_temp/` temporary folder. `audio_temp/` is temporary and not suitable for long-term storage. **If you still need the text file later, please copy or save it to another folder.**

## 4. What Languages Can Be Input?
VoiceCapsule uses the Whisper model, which can recognize multiple languages and auto-detect the source language. For example: Speak Chinese → Recognized as Chinese, Speak Japanese → Japanese, Speak Vietnamese → Vietnamese. The Chinese UI is just the interface language, not a limitation.

## 5. Speech Recognition Accuracy
Factors: Microphone quality, Distance, Environmental noise, Room echo, Speaking speed, Accent and pronunciation, Multiple people speaking, Actual recording quality. Use a better microphone and minimize noise.

## 6. Audio & Video to Text

### Basic Operation
1. Open the "Audio to Text - Video to Text" operation window.
2. Click "Select File".
3. Choose the audio or video to process.
4. Select the desired function.
5. Wait for completion.

To process multiple files at once, use "Batch Process Files". During processing, you can use "Cancel" to cancel.

### Audio/Video Output Formats
| Format | Description | Use Case |
|---|---|---|
| TXT | Plain transcript | Reading, editing, copying, archiving |
| SRT | Subtitle with time info | Video subtitles, editing, post-production |
| LRC | Lyric/text with timeline | Lyric creation and time-aligned text |

Results are stored in the `logs/` folder.

### Chinese to English Translation
Uses Whisper's speech translation capability, not simply passing already-generated Chinese text to a translator.

## 7. Folder and Temporary File Management

### `audio_temp/`: Microphone Recordings & Temp Data
Stores WAV, TXT, and related temp data. When you do audio-to-text or video-to-text, VoiceCapsule cleans up temp data after each file. Therefore, existing files in `audio_temp/` may be deleted. **Important: If the text is still needed, please copy it elsewhere first.**

### `logs/`: Audio/Video Transcription Results & Logs
Used to save text files and logs from audio/video processing. Cleaning up working temp files will not automatically empty entire `logs/`.

### Trash Button in System Settings
Will clear related saved data, including files in `logs/`. **Before pressing clear, back up.**

## 8. Auto Resource Cleanup and "Reset Memory"
**Finish one file → Clean temp data → Release resources → Process next file.**

### What "Reset Memory" Does
- Release currently loaded model.
- Release releasable RAM.
- When using GPU, release releasable VRAM.
- Release resources used by processing.
- Clean related working temp files.

After execution, model needs to be reloaded. OS may retain some allocated memory.

## 9. Text Input to Other Apps
Text can be typed into other apps that accept text input: Browsers, Word, Google Docs, Notion, Email, Code editors, Note-taking apps, etc. Place cursor in target app first. Linux currently only supports X11, Wayland planned.

### Right-Click Menu in Text Window
Copy selected, Copy all, Select all, Paste, Clear, Close window.

## 10. Common Errors & Personal Dictionary Correction

Two dictionaries:
- `common_errors.json`
- `personal_dict.json`

### `common_errors.json` Example:
```json
{
  "康菲": "ComfyUI",
  "烏班圖": "Ubuntu",
  "拍森": "Python",
  "皮特": "PyQt",
  "吉特": "Git",
  "庫比": "Qubes",
  "裏눅斯": "Linux"
}
```

### `personal_dict.json` Example:
```json
{
  "因該": "應該",
  "因位": "因為",
  "以經": "已經",
  "戰存黨": "暫存檔",
  "華鼠": "滑鼠"
}
```

Workflow: **Speak → Check result → Find fixed errors → Add to dictionary → Correct via dictionary in future.**

Basic format: `{"error text": "correct text"}`

**Note: Dictionary correction only applies to recognition flows that have integrated this feature. Batch transcription flow has not yet integrated it.**

## 11. Whisper Models
VoiceCapsule uses OpenAI Whisper family via Faster-Whisper / CTranslate2.

- small, medium, large-v3, large-v3-turbo

### small: Daily input, faster.
### medium: Balance speed & capability, supports translation.
### large-v3: ~3.1GB, best quality.
### large-v3-turbo: Fast transcription, for audio/video, not for translation.

| Use Case | Recommended Model |
|---|---|
| Daily voice input | small |
| Balance speed & capability | medium |
| Prioritize quality | large-v3 |
| Fast processing large audio/video | large-v3-turbo |

## 12. First Use of Model is Slower
First use requires loading model, so first launch/recognition may be slower. Keeping model loaded avoids reloading.

## 13. Models and Hardware
Selects execution method according to hardware. With NVIDIA CUDA GPU, can use GPU. About 3.5 GB VRAM is important reference for CUDA float16 vs CPU int8.

Factors: CPU, RAM, GPU, VRAM, Model size, Recording length, File format.

**Whether a model can run and how fast it runs are two different things.**

## 14. Chinese Traditional/Simplified Conversion
Recognition language and UI language are separate. OpenCC conversion is post-processing.

## 15. Translation Features
- General Speech Recognition: Chinese speech → Chinese text
- Whisper Speech Translation: Chinese audio → English text
**Note: large-v3-turbo mainly for fast transcription, not for translation.**

## 16. API & Online AI Features
Full version integrates:
- OpenAI, Google, Microsoft Azure, Deepgram, AssemblyAI

Full users provide own API Key, model, account settings. VoiceCapsule does not charge monthly fee for third-party APIs.

## 17. Privacy & Offline-First
### Local Mode
- Uses local Faster-Whisper models.
- No need for paid cloud speech services.
- Data processed locally, stays on device.

### Online Mode
If using API, data processed according to selected third-party API's method.

**Local Mode: Data stays on your device.**
**Online Mode: Data processed according to your chosen third-party API.**

## 18. Main Folders
| Folder/File | Purpose |
|---|---|
| `audio_temp/` | Mic recordings, recognition text, temp |
| `logs/` | Audio/video transcription results |
| `dicts/` | Common errors & personal dictionaries |
| `fonts/` | UI font files |
| `models/` | Faster-Whisper models |
| `ui/icon/` | UI icons |
| `config.json` | User preferences |

`audio_temp/` and `logs/` have different purposes. Cleaning working temp will not automatically empty entire `logs/`.

## 19. UI Operations

### 19.1 License Activation
1. Enter license key. 2. Click "Confirm Activation". 3. Window closes.

### 19.2 Main Capsule Window - Always On Top
Always on top, stays above other windows.

Right-click menu:
- **Help:** Open `README.md`.
- **About:** Show version info.
- **Exit:** Exit program.

### 19.3 Text Output Window
Right-click: Copy selected, Copy all, Select all, Paste, Clear, Close.

### 19.4 Audio/Video Processing Window
| Button | Function |
|---|---|
| Select File | Select file to process |
| Exit Settings | Close window |
| Audio to Text | Convert audio speech to text |
| Video to Text | Convert video speech to text |
| Batch Process Files | Select multiple files |
| Chinese to English | Use speech translation to English |
| Reset Memory | Release memory & resources |
| Cancel | Cancel running job |

Output formats: TXT, SRT, LRC

### 19.5 System Settings Window
- Model selection, Theme selection, Online settings, Offline mode, Text output window toggle, Recording minutes/seconds, Clear archive, Show system info, Show model info, Show theme info, Show current mode, Save, Exit

Default recording 10 seconds, minutes 0. Default offline mode, text window open.

**Clear archive will clear saved data including files in `logs/`. Back up before.**

### 19.6 API Settings Window (Full)
Service provider, API model, API Key, File selection, Processing method, Batch, Chinese to English, Real-time streaming, Test connection, Save, Exit.

## 20. Free vs Full

### Free Version - Long-term usable
- Mic voice to text, unlimited times, adjustable time, can stop early, auto detection, fixed small model, common error correction, personal dictionary, input to other software, audio/video to text, TXT/SRT/LRC, translation to English.

Daily limit for audio/video: **20 minutes cumulative per day.** This is cumulative, not single file limit, nor file count limit. Mic input not limited. Fixed small model, no API, no future updates.

If you only need basic mic input, Free may be enough.

### Full Version - NT$299 One-time
- Multiple Whisper models, Audio/video to text, TXT/SRT/LRC, Audio/video translation to English, Complete API settings, Provide third-party API Key yourself, Maintenance & updates per Full version policy.

**NT$299 one-time purchase.** Third-party API costs paid by user's own account.

V1 was open-source; V2 continues to improve with more features.

## 21. Important Reminders
1. Mic WAV & TXT in `audio_temp/`, temp only.
2. When processing audio/video, program auto cleans temp and releases resources after each file.
3. If text in `audio_temp/` still needed, copy/save elsewhere.
4. Transcription results in `logs/`, separate from `audio_temp/`.
5. Clear archive in System Settings will clear data including `logs/`. Back up before.
6. "Reset Memory" is more complete resource release, not same as clear archive.
7. Before using online APIs, confirm provider, API Key, model, usage, costs.
8. Recognition results may have errors. For important/official documents, check and save yourself.

## Conclusion
Core is simple: **Don't want to type, just speak.**

General input converts speech to text; audio/video also converts to transcripts and subtitles via local recognition.

Common terms and errors can be improved via dictionary; own accent and common words can be organized into personal dictionary.

VoiceCapsule values local execution, offline-first, privacy, while providing different models and features for work, study, creation needs.

It is not just converting sound into text, but hopes to be a convenient, lightweight tool integrating into daily work.
