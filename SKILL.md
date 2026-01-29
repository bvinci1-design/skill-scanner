# Skill Scanner

## Metadata
- **Name:** skill-scanner
- **Version:** 1.0.0
- **Author:** bvinci1-design
- **Description:** Security audit tool for Clawdbot/MCP skills - scans for malware, spyware, crypto-mining, and malicious patterns
- **Category:** Security / Development Tools
- **License:** MIT

## Capabilities
- Scan skill folders for security threats
- Detect data exfiltration patterns
- Identify system modification attempts
- Catch crypto-mining indicators
- Flag arbitrary code execution risks
- Find backdoors and obfuscation techniques
- Output reports in Markdown or JSON format
- Provide Web UI via Streamlit

## Usage

### Command Line
```bash
python skill_scanner.py /path/to/skill-folder
```

### Within Clawdbot
```
"Scan the [skill-name] skill for security issues using skill-scanner"
"Use skill-scanner to check the youtube-watcher skill"
"Run a security audit on the remotion skill"
```

### Web UI
```bash
pip install streamlit
streamlit run streamlit_ui.py
```

## Requirements
- Python 3.7+
- No additional dependencies (uses Python standard library)
- Streamlit (optional, for Web UI)

## Entry Point
- **CLI:** `skill_scanner.py`
- **Web UI:** `streamlit_ui.py`

## Tags
`security` `audit` `scanner` `malware` `spyware` `crypto-mining` `code-analysis` `mcp` `clawdbot`
