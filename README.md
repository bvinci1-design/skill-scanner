# Skill Scanner

Security audit tool for Clawdbot/MCP skills - scans for malware, spyware, crypto-mining, and malicious patterns.

## Features

- Detects **data exfiltration** patterns (env scraping, credential access, HTTP POST to unknown domains)
- Identifies **system modification** attempts (dangerous rm, crontab changes, systemd persistence)
- Catches **crypto-mining** indicators (xmrig, mining pools, wallet addresses)
- Flags **arbitrary code execution** risks (eval, exec, download-and-execute)
- Detects **backdoors** (reverse shells, socket servers)
- Finds **obfuscation** techniques (base64 decode + exec)
- Outputs **Markdown** or **JSON** reports
- Returns exit codes for CI/CD integration

## Installation

```bash
# Clone the repo
git clone https://github.com/bvinci1-design/skill-scanner.git
cd skill-scanner

# No dependencies required - uses Python standard library only
# Requires Python 3.7+
```

## Usage

### Basic scan

```bash
python skill_scanner.py /path/to/skill-folder
```

### Output to file

```bash
python skill_scanner.py /path/to/skill-folder --output report.md
```

### JSON output

```bash
python skill_scanner.py /path/to/skill-folder --json
```

### Example output

```markdown
# Skill Security Review - youtube-watcher 1.0.0

**Scan Date:** 2026-01-29T08:30:00
**Skill Path:** `/home/user/.clawdbot/skills/youtube-watcher`

## Verdict

**APPROVED** - No critical or high-severity issues detected

## Metadata

- **Name:** youtube-watcher
- **Version:** 1.0.0
- **Author:** michael gathara
- **Has SKILL.md:** True
- **Files:** 2
- **Scripts:** 1
- **Total Lines:** 89

## Findings

No security issues detected.
```

## Exit Codes

| Code | Meaning |
|------|--------|
| 0 | Approved - no issues |
| 1 | Caution - high-severity issues |
| 2 | Reject - critical issues |

## Threat Patterns Detected

### Critical (auto-reject)
- Credential path access (~/.ssh, ~/.aws, /etc/passwd)
- Dangerous recursive delete (rm -rf /)
- Systemd/launchd persistence
- Crypto miners (xmrig, ethminer, stratum+tcp)
- Download and execute (curl | sh)
- Reverse shells (/dev/tcp, nc -e)
- Base64 decode + exec obfuscation

### High (caution)
- Bulk environment variable access
- Crontab modification
- eval/exec dynamic code execution
- Socket servers

### Medium (informational)
- Environment variable reads
- HTTP POST to external endpoints

## CI/CD Integration

```yaml
# GitHub Actions example
- name: Scan skill for security issues
  run: |
    python skill_scanner.py ./my-skill --output scan-report.md
    if [ $? -eq 2 ]; then
      echo "CRITICAL issues found - blocking merge"
      exit 1
    fi
```

## Contributing

Pull requests welcome! To add new threat patterns, edit the `THREAT_PATTERNS` list in `skill_scanner.py`.

## License

MIT
