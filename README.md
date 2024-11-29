# Summary Scraper

**Summary Scraper** is a Python tool designed to fetch YouTube video transcripts or transcribe audio files using OpenAI's Whisper model. It uses Natural Language Processing (NLP) techniques to detect the language of the content, translate it if necessary, and generate concise summaries using the Pegasus model.

## Features

- Fetches YouTube video transcripts (if available).
- Uses Whisper for transcribing audio content.
- Detects the language of the transcript and translates it into English (optional).
- Summarizes the content with the Pegasus model.
- Handles long-form content efficiently by splitting it into manageable chunks for summarization.

## Requirements

Before you begin, make sure you have the following installed:

- Python 3.7 or higher
- pip (for installing dependencies)

## Dependencies

Here’s a list of the required Python dependencies:

- `youtube-transcript-api`: To fetch YouTube video transcripts.
- `whisper`: OpenAI's Whisper model for audio transcription.
- `transformers`: For text summarization using the Pegasus model.
- `langdetect`: For language detection to determine the language of the transcript.
- `deep-translator`: For translating non-English transcripts to English (optional).
- `requests`: For making HTTP requests (used by some libraries).
- `torch`: PyTorch, required by Whisper and transformers.

You can install all the dependencies by running the following:

```bash
pip install -r requirements.txt 

## How It Works

### 1. **Transcript Fetching**:
   - The tool first attempts to fetch the transcript of a YouTube video using the `youtube-transcript-api`. If the video has captions enabled, it retrieves the available transcript.
   - If a transcript is not available (i.e., the video doesn't have captions or transcripts), the tool proceeds to transcribe audio files directly.

### 2. **Audio Transcription (If No Transcript Available)**:
   - When a YouTube transcript isn't available, the tool uses **Whisper**, an automatic speech recognition (ASR) model by OpenAI, to transcribe audio content. 
   - Whisper works with various audio formats (MP3, MP4, WAV, etc.), making it versatile for different types of media.
   - The audio file is processed to generate text from speech, which can then be further analyzed and summarized.

### 3. **Language Detection**:
   - After fetching or transcribing the content, the tool uses the `langdetect` library to automatically detect the language of the text.
   - This step is essential because the content might not be in English. The tool identifies the language to decide whether translation is needed.

### 4. **Translation (If Non-English)**:
   - If the detected language is not English, the tool uses the **deep-translator** library to translate the text into English.
   - Translation ensures that the content is processed and summarized in English, regardless of the original language, so you can still get accurate and coherent summaries.

### 5. **Summarization**:
   - The translated (or original English) text is passed to the **Pegasus** model, which is a transformer-based model for text summarization. 
   - The **transformers** library from Hugging Face is used to run the Pegasus model.
   - For long-form content, the tool splits the text into smaller chunks to avoid exceeding model input limits. Each chunk is summarized separately, and the summaries are then combined to produce a final, cohesive summary.

### 6. **Final Output**:
   - The tool outputs a concise, human-readable summary of the content.
   - The summary focuses on the most important points and key takeaways, reducing long-form content into a brief yet comprehensive overview.

