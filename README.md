# AI Visa Assistant 🛂

An AI-powered solution to determine visa requirements between countries using OpenAI's GPT models and function calling.

## Project Objective 🎯
**Primary Goal:** Determine visa type and maximum stay duration for a given passport nationality and destination country based on provided visa rules data.

**Key Features:**
- Visa requirement analysis using OpenAI GPT-4/GPT-4o-mini
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
git clone https://github.com/HopeforgeDev/Visa-Assistant.git
cd Visa-Assistant

# Install dependencies
pip install openai ipywidgets pillow python-dotenv

jupyter nbextension enable --py widgetsnbextension

# For JupyterLab users
jupyter labextension install @jupyter-widgets/jupyterlab-manager
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
...
AI: Thank you. Could you specify your passport nationality?
User: upload  # Type exactly this and press Enter
AI: Press Enter after uploading...  # Hit Enter in the notebook input field
[Presses Enter]
AI: Detected passport code: SGP
AI: Singaporean passport holders are exempt...

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
1. **Visa Recommendation Engine**
```python
def get_visa_recommendation(passport_code, destination_code):
    # Returns formatted recommendation based on exact JSON data
```

3. **Conversation Manager**
```python
def visa_chat():
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
