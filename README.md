# VideoNarratorAI
AI Video Narrator by RapidAI An advanced web application that automatically generates professional narrations for videos using artificial intelligence. 

Try it here:

https://c73e736d-0664-4646-ae74-68c1e6afe604-00-1dfpte62mystr.spock.replit.dev/

# AI Video Narrator by RapidAI

An advanced web application that automatically generates professional narration for videos using GPT-4V vision analysis and text-to-speech conversion. The system provides a seamless experience for video processing, custom narration editing, and final video generation.

## Features

- **Intelligent Video Analysis**: Utilizes GPT-4V for advanced content analysis and narration generation
- **Multiple Voice Options**: Choose from six different voice options:
  - Alloy (Neutral)
  - Echo (Warm)
  - Fable (British)
  - Onyx (Professional)
  - Nova (Friendly)
  - Shimmer (Cheerful)
- **Efficient Processing**: 
  - Chunked video processing for handling longer videos
  - Optimized frame extraction
  - Memory management and rate limiting
- **Real-time Preview**: Live video preview with synchronized audio
- **Custom Script Editing**: Edit and update narration scripts with real-time preview
- **Secure File Handling**: Verified upload/download operations with proper error management

## Installation

1. Clone the repository
2. Set up environment variables:
   ```
   OPENAI_API_KEY=your_openai_api_key
   ```
3. Install dependencies:
   ```bash
   pip install flask flask-sqlalchemy opencv-python openai moviepy requests
   ```
4. Initialize the database:
   ```bash
   python
   >>> from app import db
   >>> db.create_all()
   ```

## Usage

1. Start the server:
   ```bash
   python main.py
   ```
2. Access the web interface at `http://localhost:5000`
3. Upload a video (supported formats: MP4, AVI, MOV, WMV)
4. Select your preferred voice
5. Click "Generate Narration"
6. Edit the generated script if needed
7. Preview and download the final narrated video

## API Endpoints

### POST /upload
Upload a video for narration generation.
- Body: multipart/form-data
  - video: Video file (required)
  - voice: Voice option (default: "onyx")
- Returns: JSON with script and output path

### POST /update_narration
Update the narration script for a processed video.
- Body: JSON
  - script: New narration text
  - video_id: ID of the processed video
- Returns: JSON with updated script and output path

### GET /download/<filename>
Download the processed video.
- Parameters:
  - filename: Name of the processed video file
- Returns: Video file download

## Technical Details

### Video Processing Pipeline

1. **Frame Extraction**
   - Optimized frame selection using intervals
   - Memory-efficient processing with chunking
   - Quality optimization for large videos

2. **Content Analysis**
   - GPT-4V vision analysis for frame understanding
   - Contextual narration generation
   - Rate limit handling with exponential backoff

3. **Audio Generation**
   - Text-to-speech conversion using OpenAI's TTS API
   - Multiple voice options
   - Audio-video synchronization

4. **File Management**
   - Secure file handling
   - Automatic cleanup of temporary files
   - Progress tracking and status updates

### Database Schema

```sql
CREATE TABLE video (
    id INTEGER PRIMARY KEY,
    filename VARCHAR(255) NOT NULL,
    original_filename VARCHAR(255) NOT NULL,
    status VARCHAR(50) DEFAULT 'processing',
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    narration_text TEXT,
    output_path VARCHAR(255)
);
```

## Dependencies

- Flask: Web framework
- Flask-SQLAlchemy: Database ORM
- OpenCV: Video processing
- OpenAI: GPT-4V and TTS API
- MoviePy: Video editing
- Bootstrap: UI framework

## Error Handling

The application implements comprehensive error handling:
- File validation
- API rate limiting
- Processing failures
- Database operations
- File system operations

## Environment Variables

Required environment variables:
- `OPENAI_API_KEY`: Your OpenAI API key for GPT-4V and TTS services

## Security Considerations

- Secure file upload handling
- Path traversal prevention
- File type validation
- Size limitations (100MB max)
- Proper error messages

## License

RapidAi

AI Video Narrator by RapidAI
An advanced web application that automatically generates professional narrations for videos using artificial intelligence. The system combines GPT-4V's visual understanding capabilities with OpenAI's text-to-speech technology to create engaging video narrations.

Features
Automated video content analysis using GPT-4V
Professional narration generation in multiple voices
Support for various video formats (MP4, AVI, MOV, WMV)
Custom narration script editing
Real-time video preview with synchronized audio
Multiple voice options (Alloy, Echo, Fable, Onyx, Nova, Shimmer)
Efficient processing of longer videos through chunking
Secure file handling with size limits and format validation
Technical Features
Optimized frame extraction and video processing
Rate limiting and memory management
Comprehensive error handling
Secure file operations
Database-backed video processing queue
Client-side file validation
Requirements
Python 3.8+
OpenAI API key
FFmpeg for video processing
Usage
Upload a video (supported formats: MP4, AVI, MOV, WMV)
Select preferred narration voice
Wait for automated processing
Review and edit generated narration if desired
Preview the narrated video
Download the final video
Limitations
Maximum file size: 100MB
Processing time depends on video length
Requires stable internet connection
API rate limits apply
