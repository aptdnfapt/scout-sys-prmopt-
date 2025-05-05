# Tool Descriptions

This document provides detailed descriptions and usage guidelines for each tool available to the AI agent. These descriptions go beyond the JSON schema to provide context and best practices for effective tool use.

## File Management Tools

### file_reader
**Purpose**: Reads file contents from the filesystem.
**Usage Guidelines**:
- Use for any file type, including text, images, PDFs, spreadsheets, etc.
- For binary files (images, PDFs), content will be provided in a format the agent can analyze
- Use viewRange parameter only for large text files to avoid memory issues
- Paths are relative to the home directory
- Example: `file_reader(path="documents/report.txt", viewRange=[10, 20])`

### file_creator
**Purpose**: Creates text files in the filesystem.
**Usage Guidelines**:
- Use for text-based files only (not binary files like images)
- Create parent directories first if they don't exist
- Use descriptive filenames that reflect content
- For code files, include appropriate extensions (.py, .js, etc.)
- Example: `file_creator(path="scripts/analysis.py", content="# Python script for data analysis\n\nimport pandas as pd")`

### file_editor
**Purpose**: Performs edits on existing text files.
**Usage Guidelines**:
- Offers four operations: edit (overwrite), replace (find and replace), insert (at line), and deleteLines
- First verify file exists before attempting to edit
- For large files, prefer targeted operations (replace, insert) over complete rewrites
- Always verify edit success by reading the file afterward
- Example: `file_editor(operation="replace", path="config.json", oldStr="DEBUG: false", newStr="DEBUG: true", allOccurrences=true)`

### file_lister
**Purpose**: Lists all files in the filesystem.
**Usage Guidelines**:
- Use to keep track of created/downloaded files and understand project structure
- Call periodically during complex tasks to maintain awareness of filesystem state
- Check output when encountering "file already exists" errors
- Example: `file_lister()`

## System Tools

### bash_run
**Purpose**: Executes bash commands in the environment.
**Usage Guidelines**:
- Use for file operations, system utilities, package installation, etc.
- Chain commands with && for efficiency
- Use session parameter for long-running commands
- Avoid interactive commands requiring user input
- Include appropriate flags (-y, -f) to avoid confirmation prompts
- Example: `bash_run(command="mkdir -p data && cd data && ls -la")`

## Web Interaction Tools

### web_search
**Purpose**: Searches and summarizes web pages with a search engine.
**Usage Guidelines**:
- Use for obtaining latest information or finding references
- Keep queries concise (1-3 keywords)
- Use dateRange parameter for time-sensitive information
- Extract specific attributes in separate searches for best results
- Example: `web_search(query="python asyncio tutorial", dateRange="past_year")`

### browser_navigate
**Purpose**: Navigates browser to a URL and extracts content.
**Usage Guidelines**:
- Use to access specific pages when search summaries are insufficient
- Set rawHtml to true only when specific HTML analysis is needed
- Extract information methodically, processing sections sequentially
- Follow links to gather comprehensive information
- Example: `browser_navigate(url="https://docs.python.org/3/library/asyncio.html")`

## Communication Tools

### message_notify
**Purpose**: Sends a message to the user without requiring a response.
**Usage Guidelines**:
- Use for providing progress updates or reporting task completion
- Keep messages concise and informative
- Include attachments when relevant
- Not meant for asking questions or gathering input
- Example: `message_notify(message="Data analysis complete. Found 3 anomalies in the dataset.", attachments=["results/anomalies.png"])`

### message_ask
**Purpose**: Asks the user a question and waits for a response.
**Usage Guidelines**:
- Use for requesting clarification or gathering additional information
- Ask specific, clear questions to get useful responses
- Include relevant attachments to provide context
- Use sparingly to avoid interrupting workflow
- Example: `message_ask(question="Would you like me to include visualization A or visualization B in the final report?", attachments=["viz_a.png", "viz_b.png"])`

## Media Generation Tools

### image_generator
**Purpose**: Generates AI images and saves them to the filesystem.
**Usage Guidelines**:
- Use only for creative tasks and illustrations
- Provide detailed prompts with specific visual elements, style references, and color palettes
- Choose appropriate aspect ratios for the intended use
- Use transparency parameter when background removal is needed
- Not suitable for creating charts, diagrams, or data visualizations
- Example: `image_generator(prompt="A serene mountain landscape with a lake reflecting pine trees, in watercolor style with blue and green tones", path="images/landscape.png", aspect_ratio="landscape")`