# WhisperXAPI

WhisperXAPI is a real-time transcription and speaker diarization API built using OpenAI's Whisper, pyannote-audio, and FastAPI. The API supports both real-time audio streaming from a user's microphone and file uploads for transcription. It provides speaker-labeled transcriptions that are processed in real-time or from uploaded audio files.

## Features

- **Real-time Transcription**: Stream audio directly from a microphone for on-the-fly transcription.
- **Speaker Diarization**: Detect and label multiple speakers in the audio.
- **File Upload**: Upload audio files for batch transcription with speaker labels.
- **GPU Support**: Leverages GPU acceleration for faster processing (if available).
- **Asynchronous API**: Built with FastAPI for handling multiple concurrent requests efficiently.

## Getting Started

### Prerequisites

- **Conda** (Miniconda or Anaconda)
- **Python 3.8+**
- **Git**
- **FFmpeg** (optional, for audio handling)

### Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/your-username/whisperxapi.git
   cd whisperxapi

2. **Set up the Conda environment**:
   ```bash
   conda create -n whisperxapi_env python=3.8
   conda activate whisperxapi_env
   ```

3. **Install dependencies**:
   - Install **PyTorch** with GPU support (if available):
     ```bash
     conda install pytorch torchvision torchaudio cudatoolkit=11.3 -c pytorch
     ```
     For CPU-only installations, use:
     ```bash
     conda install pytorch torchvision torchaudio cpuonly -c pytorch
     ```

   - Install **FastAPI**, **WhisperX**, and **pyannote-audio**:
     ```bash
     pip install fastapi uvicorn
     pip install git+https://github.com/m-bain/whisperX.git
     pip install pyannote-audio
     ```

   - Optionally, install **FFmpeg** for handling audio processing:
     ```bash
     conda install -c conda-forge ffmpeg
     ```

### Running the API

1. **Start the FastAPI server**:
   ```bash
   uvicorn main:app --reload
   ```

2. **Access the API documentation**:
   Once the server is running, navigate to `http://127.0.0.1:8000/docs` in your browser to interact with the API's Swagger-generated documentation.

### API Endpoints

- **POST `/transcribe/stream`**: Accepts audio streamed from the user's microphone and returns real-time transcription and diarization.
- **POST `/transcribe/upload`**: Accepts uploaded audio files (e.g., WAV, MP3) for transcription and diarization.

### Example Request for File Upload

You can use a tool like `curl` to test the file upload functionality:

```bash
curl -X 'POST' \
  'http://127.0.0.1:8000/transcribe/upload' \
  -H 'accept: application/json' \
  -H 'Content-Type: multipart/form-data' \
  -F 'audio_file=@path_to_audio_file.wav'
```

### Usage

WhisperXAPI can be used for various applications that require transcription and diarization, such as:
- Real-time transcription for meetings, lectures, or interviews.
- Automatic content creation for podcasts, videos, and other media.
- Customer support transcription for call centers.

### Project Structure

```plaintext
whisperxapi/
├── main.py            # Main FastAPI application
├── test_env.py        # Environment test script
├── requirements.txt   # Dependencies list
└── README.md          # Project documentation
```

### License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
