# AI Visa Assistant 🛂

An AI-powered solution to determine visa requirements between countries using OpenAI's GPT models and function calling.

## Project Objective 🎯
**Primary Goal:** Determine visa type and maximum stay duration for a given passport nationality and destination country based on provided visa rules data.

**Key Features:**
- Visa requirement analysis using OpenAI GPT-4/GPT-4o
- Text and image input support for passport information
- Structured conversation flow matching real consular interactions
- Strict validation against provided JSON data schema

## Prerequisites 📋
- Python 3.9+
- Jupyter Notebook
- OpenAI API key (provided separately)
- Basic understanding of ISO country codes (3-letter format)

## Setup Instructions ⚙️

### 1. Environment Setup
```bash
# Clone repository
git clone https://github.com/yourusername/visa-assistant.git
cd visa-assistant

# Install dependencies
pip install openai ipywidgets pillow python-dotenv
```

### 2. Configuration
1. Create `.env` file:
```bash
echo "OPENAI_API_KEY=your_api_key_here" > .env
```

2. Place these files in project root:
- `visa_information.json` (provided dataset)
- `specimen-passports/` directory (for image upload testing)

### 3. Data Structure Validation
Ensure your `visa_information.json` follows this structure:
```json
{
  "PRT": {
    "visaFree": {
      "SGP": {"maxStay": 30}
    },
    "visaOnArrival": {
      "CYP": {"maxStay": 90}
    }
  }
}
```

## Usage Instructions 💻

### Basic Text-Based Flow
1. Start Jupyter Notebook:
```bash
jupyter notebook
```

2. Open `visa_assistant.ipynb`

3. Follow prompts:
```text
AI: Welcome to Visa Assistant! How can I help today?
User: I'm planning a trip to Portugal
AI: Could you please specify your passport issuer?
User: Lebanon
AI: Lebanese passport holders need to apply for a visa...
```

### Image Upload Flow (Bonus)
1. In the notebook interface:
```text
AI: Could you please specify your passport issuer?
Click "Upload Passport" button and select image
AI: Detected Singaporean passport. Visa exempt for 30 days.
```

2. Supported passport images:
- Machine-readable zone (bottom of passport page)
- Clear country code visibility

## Project Structure 📂
```
visa-assistant/
├── Visa_Assistant.ipynb        # Main notebook
├── visa_information.json       # Visa rules dataset
├── .env.example                # Environment template
├── requirements.txt            # Dependency list
└── specimen-passports/         # Sample passport images
    ├── portugal.jpg
    └── singapore.jpg
```

## Key Functionality 🔧
1. **Visa Rules Engine**
```python
def check_visa_requirements(passport_code, destination_code):
    # Core logic matching JSON structure
    # Returns visaFree/visaOnArrival/visaRequired
```

2. **Image Processing**
```python
def extract_passport_country(image_content):
    # Uses GPT-4 Vision to read passport MRZ
    # Returns 3-letter ISO code
```

3. **Conversation Manager**
```python
def handle_conversation():
    # Manages state: Destination -> Passport -> Result
    # Implements exact sample dialogue patterns
```

## Testing Scenarios 🧪
| Test Case | Input | Expected Output |
|-----------|-------|-----------------|
| Lebanese → Portugal | LBN/PRT | Apply offline |
| Singaporean → Portugal | SGP/PRT | Visa exempt 30 days |
| Cypriot → Portugal | CYP/PRT | Visa on arrival 90 days |
| Image Upload Test | passport.jpg | Detected country code |
