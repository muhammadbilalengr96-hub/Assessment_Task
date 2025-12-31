# Markdown Meeting Notes → Google Docs Converter

## Overview

This project provides a **Python script designed for Google Colab** that converts structured **Markdown meeting notes** into a **well-formatted Google Doc** using the **Google Docs API**.

The script programmatically:
- Creates a new Google Doc  
- Applies proper heading styles (H1 / H2 / H3)  
- Preserves nested bullet-point hierarchy  
- Converts Markdown checkboxes (`- [ ]`) into real Google Docs checkboxes  
- Highlights assignee mentions (e.g. `@sarah`)  
- Formats footer metadata (recorded by, duration) distinctly  

This solution is ideal for **product teams, engineering syncs, sprint reviews, and meeting automation workflows**.
---

## Features
- Google Docs API integration  
- Automatic document creation  
- Markdown-to-Google-Docs formatting conversion  
- Nested bullets with indentation  
- Checkbox support  
- Styled `@mentions`  
- Colab-friendly authentication  
- Error handling and readable code structure  
---

## Requirements

### Google Account
- A Google account with access to **Google Docs**
- Permission to authenticate in **Google Colab**

### Python Environment
- This project is intended to run in **Google Colab**
- No local setup is required

---

## Required Dependencies

The script relies on the following Python libraries:
- `google-api-python-client`
- `google-auth`
- `google-auth-httplib2`
- `google-auth-oauthlib`

> All dependencies are installed automatically within Google Colab.

---

## Setup Instructions (Google Colab)

### 1. Open Google Colab
Navigate to:  
https://colab.research.google.com

Create a **new Python notebook**.

---

### 2. Install Dependencies

Run the following cell:

!pip install --quiet google-api-python-client google-auth-httplib2 google-auth-oauthlib

3. Authenticate with Google
Run the following cell and complete the authentication prompt:

from google.colab import auth
auth.authenticate_user()

from googleapiclient.discovery import build
from google.auth import default

creds, _ = default()
docs_service = build('docs', 'v1', credentials=creds)
This grants the notebook permission to create and edit Google Docs in your account.

How to Run the Script in Colab
1. Define the Markdown Input
Provide your meeting notes as a Markdown string:

MARKDOWN_TEXT = """
# Product Team Sync - May 15, 2023
## Attendees
- Sarah Chen (Product Lead)
- Mike Johnson (Engineering)
...
"""

2. Run the Conversion Function
Call the conversion function:

doc_url = create_google_doc_from_markdown(MARKDOWN_TEXT)
doc_url

3. Open the Generated Google Doc
The function returns a URL to the newly created Google Doc.

Click the link to view, edit, and share your formatted document.

## Output Formatting Details

| Markdown Element | Google Docs Result |
|---|---|
| `# Title` | Heading 1 |
| `## Section` | Heading 2 |
| `### Subsection` | Heading 3 |
| `* Item` | Bulleted list |
| Nested bullets | Indented bullets |
| `- [ ] Task` | Checkbox |
| `@username` | Bold + colored text |
| Footer notes | Small, italic text |


Error Handling
- API errors are caught and raised with clear messages
- Invalid Google Docs API values (e.g. unsupported bullet presets) are avoided
- Batch update operations are executed safely

Notes & Limitations
- Designed for structured Markdown, not arbitrary Markdown files
- Tables, images, and hyperlinks are not currently supported
- Bullet indentation is derived from leading spaces

Possible Extensions
- Read Markdown from a file
- Automatically share the generated Google Doc
- Support tables and links
- Convert multiple notes in batch
- Package as a reusable Python module