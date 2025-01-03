# Whisper - Speech Recognition with Python

Whisper is an open-source, general-purpose speech recognition model developed by OpenAI. This README provides complete guidance on installing, using, and optimizing Whisper for various speech recognition tasks.

---

## Features
- **Transcription**: Converts speech in audio files into text.
- **Language Detection**: Identifies the spoken language in audio.
- **Translation**: Translates non-English speech into English.
- **Timestamps**: Provides timestamps for each word or segment.

---

## Installation

### Install Python Package
To use Whisper, install the `whisper` Python package and `ffmpeg` for audio processing:

```bash
pip install whisper
pip install ffmpeg-python
```

### Install `ffmpeg`

#### Ubuntu/Debian:
```bash
sudo apt install ffmpeg
```

#### MacOS:
```bash
brew install ffmpeg
```

#### Windows:
1. Download `ffmpeg` from [ffmpeg.org](https://ffmpeg.org/download.html).
2. Add it to your system's PATH.

---

## Model Variants

Whisper provides models of different sizes. Select a model based on your accuracy and performance requirements:

| Model Name | Parameters | Speed (Relative to Base) | Capabilities            |
|------------|------------|--------------------------|-------------------------|
| Tiny       | 39M        | 32x faster              | Basic transcription     |
| Base       | 74M        | 16x faster              | Good for small tasks    |
| Small      | 244M       | 6x faster               | Higher accuracy         |
| Medium     | 769M       | 2x faster               | Multilingual support    |
| Large      | 1550M      | 1x (slowest)            | Best accuracy & features|

---

## Basic Usage

### Load the Model
```python
import whisper

model = whisper.load_model("base")  # Load a model variant
```

### Transcribe Audio
```python
result = model.transcribe("audio_file.mp3")
print("Transcription:", result["text"])
```

---

## Advanced Features

### Specify Language
To improve accuracy, you can specify the language manually:
```python
result = model.transcribe("audio_file.mp3", language="en")
```

### Translate to English
Translate non-English speech into English:
```python
result = model.transcribe("audio_file.mp3", task="translate")
print("Translation:", result["text"])
```

### Retrieve Timestamps
Get timestamps for words or phrases:
```python
for segment in result["segments"]:
    print(segment["start"], segment["end"], segment["text"])
```

### Run on GPU
To accelerate transcription, run the model on a GPU:
```python
model = whisper.load_model("base").to("cuda")
```

---

## Audio Preprocessing
Whisper expects audio in a standard format (e.g., `.mp3`, `.wav`). Convert files using `ffmpeg` if necessary:
```bash
ffmpeg -i input_video.mp4 -ar 16000 -ac 1 output_audio.wav
```

---

## Complete Workflow Example

Here’s a full script demonstrating transcription, translation, and timestamps:

```python
import whisper

# Load Whisper model
model = whisper.load_model("medium")

# Transcribe audio file
audio_path = "sample_audio.mp3"
result = model.transcribe(audio_path)

# Print transcription
print("Transcription:")
print(result["text"])

# Print translation (if audio is non-English)
translation_result = model.transcribe(audio_path, task="translate")
print("\nTranslation to English:")
print(translation_result["text"])

# Print timestamps for each segment
print("\nTimestamps:")
for segment in result["segments"]:
    print(f"[{segment['start']} - {segment['end']}] {segment['text']}")
```

---

## Common Errors and Solutions

### Error: `"ffmpeg not found"`
Ensure `ffmpeg` is installed and added to your PATH.

### Error: `"CUDA out of memory"`
Reduce the model size or run the model on CPU instead of GPU.

### Error: `"File not found"`
Check the audio file path and ensure it exists.

---

## Applications
- **Content Creation**: Generate subtitles for videos automatically.
- **Accessibility**: Transcribe audio for the hearing impaired.
- **Education**: Analyze lecture recordings or podcasts.
- **Customer Support**: Transcribe and analyze customer calls.
- **Multilingual Support**: Handle audio in diverse languages.

---

## Resources
- [Whisper GitHub Repository](https://github.com/openai/whisper)
- [FFmpeg Documentation](https://ffmpeg.org/documentation.html)

---

Enjoy using Whisper for all your speech recognition tasks! If you encounter any issues or have questions, feel free to reach out.
