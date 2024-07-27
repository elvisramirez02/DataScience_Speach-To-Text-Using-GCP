# 🗣️ Speech-to-Text with Google Cloud Platform (GCP) 🗣️

## 📋 Project Overview

This project demonstrates how to use Google Cloud Platform (GCP) to convert speech to text. The aim is to process audio files, extract text data, and perform sentiment and NLP analysis. This README will guide you through the steps taken and highlight the ML and DS skills used, as well as mention equivalent services from Azure and AWS.

## 🚀 Activities Performed

### 1. Set Up Credentials for GCP 🔐
- Configured GCP credentials to access the Google Cloud services.

### 2. Create a Bucket to Save Data 🪣
- Created a Google Cloud Storage bucket to store audio files.

### 3. Convert Audio File to WAV Format 🎶
- Ensured the audio file was in WAV format for compatibility.

### 4. Load Data into GCP Bucket 📤
- Uploaded the audio file to the GCP bucket.

### 5. Apply Speech-to-Text Using Different Options 🗣️➡️💬
- Utilized GCP’s Speech-to-Text API to transcribe the audio file.

#### 5.1 Using URI Method
```python
from google.cloud import speech

def run_quickstart() -> speech.RecognizeResponse:
    client = speech.SpeechClient()
    transcripts = []
    gcs_uri = "gs://my_newbucketslc3/test.wav"
    audio = speech.RecognitionAudio(uri=gcs_uri)
    config = speech.RecognitionConfig(
        encoding=speech.RecognitionConfig.AudioEncoding.LINEAR16,
        sample_rate_hertz=44100,
        audio_channel_count=2,
        language_code="en-US",
    )
    operation = client.long_running_recognize(config=config, audio=audio)
    print("Waiting for operation to complete...")
    response = operation.result()
    for result in response.results:
        print(f"Transcript: {result.alternatives[0].transcript}")
        transcript = result.alternatives[0].transcript
        transcripts.append(transcript)
    return transcripts

text = run_quickstart()
```

#### 5.2 Using Local File Method
```python
from google.cloud import speech

client = speech.SpeechClient()
with open("test.wav", "rb") as audio_file:
    content = audio_file.read()

audio = speech.RecognitionAudio(content=content)
config = speech.RecognitionConfig(
    encoding=speech.RecognitionConfig.AudioEncoding.LINEAR16,
    sample_rate_hertz=44100,
    audio_channel_count=2,
    language_code="en-US",
)

response = client.recognize(config=config, audio=audio)
for result in response.results:
    print("Transcript: {}".format(result.alternatives[0].transcript))
```

### 6. Save Extracted Text Data into Firestore 📄➡️🔥
- Saved the transcribed text data into a NoSQL Firestore database.

### 7. Upload Dictionary to Firestore 📤
- Uploaded the dictionary containing transcribed data to Firestore.

### 8. Read Data from Firestore 📥
- Retrieved data from Firestore for further analysis.

### 9. Sentiment and NLP Analysis 🧠📈
- Performed sentiment and natural language processing (NLP) analysis on the transcribed text.

### 10. Show Findings Through Visualizations 📊
- Visualized the findings from the sentiment and NLP analysis.

## 🌐 Cloud Services Comparison

### Google Cloud Platform (GCP)
- **Speech-to-Text API**: Converts audio to text with high accuracy.
- **Cloud Storage**: Stores audio files and other data.
- **Firestore**: NoSQL database to store and retrieve text data.

### Amazon Web Services (AWS)
- **Transcribe**: Converts speech to text.
- **S3 (Simple Storage Service)**: Stores audio files.
- **DynamoDB**: NoSQL database for storing transcribed text.

### Microsoft Azure
- **Cognitive Services - Speech**: Converts audio to text.
- **Blob Storage**: Stores audio files.
- **Cosmos DB**: NoSQL database for storing text data.

## 🏢 Use Cases for Businesses

### Customer Support 📞
- **Automate Transcription**: Convert support call recordings to text for quality analysis and training.
- **Sentiment Analysis**: Analyze customer emotions and satisfaction levels.

### Market Research 📊
- **Voice Surveys**: Transcribe and analyze voice survey responses.
- **Public Opinion**: Monitor and analyze spoken feedback on products.

### Healthcare 🏥
- **Medical Records**: Transcribe doctor-patient conversations for accurate record-keeping.
- **Patient Feedback**: Analyze patient reviews and feedback.

### Media & Entertainment 🎬
- **Subtitles & Captions**: Automatically generate subtitles and captions for videos.
- **Content Analysis**: Analyze spoken content for insights and trends.

## 🌟 Benefits for Managers

### Enhanced Decision Making
- Data-driven insights from transcriptions help in making informed business decisions.

### Improved Customer Experience
- Understanding customer sentiment and feedback leads to better service and product improvements.

### Efficiency & Automation
- Automating transcription and analysis saves time and resources, allowing teams to focus on strategic tasks.
