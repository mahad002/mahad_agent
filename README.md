# Voice-Based Customer Service Assistant

A voice-enabled customer service system that can handle meeting scheduling, product inquiries, and general store information using speech recognition and text-to-speech capabilities.

## Core Features

### Voice Interaction
- Uses Deepgram for Speech-to-Text (STT)
- Uses ElevenLabs for Text-to-Speech (TTS)
- Handles continuous conversation until user says "exit" or "goodbye"
- Web interface with real-time conversation display

### Meeting Scheduling System
1. **Conversation State Tracking**
   - Maintains context of the conversation
   - Tracks selected staff member and scheduling progress

2. **Time Processing**
   - Extracts time from natural language input
   - Normalizes various time formats (e.g., "9pm", "9:00 PM", "nine in the evening")
   - Matches normalized times with staff availability

3. **Meeting Storage**
   - Generates unique meeting IDs
   - Stores meetings as JSON files in the meetings directory

### Data Management
- Loads store information from `description.json`
- Loads product catalog from `products.json`
- Loads staff details and availability from `staff.json`
- Maintains conversation history

## Key Components

### Time Handling
```python
def normalize_time(self, time_str):
    # Converts various time formats to standard "HH:MM AM/PM"
    # Examples: "9pm" → "9:00 PM", "14:00" → "2:00 PM"

def extract_time_from_text(self, text):
    # Extracts time from natural language sentences
    # Example: "meeting at 9pm" → "9:00 PM"
```

### Meeting Scheduling Flow
1. User mentions "meeting"
2. System displays available staff
3. User specifies staff member
4. System shows available times
5. User specifies time
6. System confirms and stores meeting

### Web Interface
- Start/End call buttons for controlling the conversation
- Real-time display of transcribed user input
- Display of system responses
- Visual indication of call status
- Handles edge cases like no speech detected

## How to Run

### 1. Install Dependencies
```bash
pip install flask flask-cors python-dotenv openai pygame SpeechRecognition deepgram requests
```

### 2. Set Up Environment Variables
Create a `.env` file with:
```
ELEVEN_LABS_API_KEY=your_elevenlabs_api_key
ELEVEN_LABS_VOICE_ID=your_elevenlabs_voice_id
OPENAI_API_KEY=your_openai_api_key
DEEPGRAM_API_KEY=your_deepgram_api_key
```

### 3. Prepare Data Files
Ensure you have:
- `description.json` - Store information
- `products.json` - Product catalog
- `staff.json` - Staff details with availability

### 4. Create Required Directories
```bash
mkdir -p logs meetings responses reviews audio_responses orders
```

### 5. Run the Application
```bash
python app.py
```

### 6. Access the Web Interface
Open your browser and go to:
```
http://localhost:5000
```

## Future Improvements

### Suggested Enhancements
1. **Name Matching**
   - Implement fuzzy string matching for staff names
   - Handle phonetic similarities (e.g., "Jackie"/"Jacky")

2. **Time Processing**
   - Add support for more time formats
   - Handle timezone specifications
   - Add meeting duration support

3. **Meeting Management**
   - Add conflict checking
   - Implement meeting modification
   - Add cancellation functionality

4. **Web Interface**
   - Add visual feedback during listening
   - Implement direct text input option
   - Add meeting history view

## Environment Setup
Required environment variables in `.env`:
- `ELEVEN_LABS_API_KEY`: For text-to-speech
- `ELEVEN_LABS_VOICE_ID`: Voice selection for TTS
- `OPENAI_API_KEY`: For natural language processing
- `DEEPGRAM_API_KEY`: For speech-to-text

## File Structure
```
project/
├── app.py                  # Main Flask application
├── description.json        # Store information
├── products.json           # Product catalog
├── staff.json              # Staff details
├── static/                 # Static files (CSS, JS)
├── templates/              # HTML templates
│   └── index.html          # Main frontend page
├── logs/                   # Log files
├── meetings/               # Stored meeting records
├── responses/              # Voice response files
├── reviews/                # Customer review storage
├── audio_responses/        # Generated audio files
└── orders/                 # Order records
```

## Troubleshooting

- **Microphone issues**: Make sure your browser has permission to access your microphone
- **API errors**: Check your `.env` file for correct API keys
- **Audio not playing**: Ensure your speakers are on and working
- **Transcription problems**: Speak clearly and check your microphone settings
- **Empty responses**: If you don't speak, the system will prompt you to try again