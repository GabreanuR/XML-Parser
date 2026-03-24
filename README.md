# Custom XML-TXT Converter (Bash)

> A bi-directional text converter built entirely in Bash, designed as an exercise in advanced shell scripting, string manipulation, and data structure implementation.

**Authors & Contributors:** * Răzvan - [Link Profil GitHub]
* Maia - [@rmig22](https://github.com/rmig22)
* Ruxi - [@maia-sapunaru](https://github.com/maia-sapunaru)

## Overview

This script provides an interactive Command Line Interface (CLI) to convert rigidly formatted XML data into an indented, human-readable TXT format, and vice-versa. 

Rather than using built-in parsing libraries, this project was built from scratch to explore the capabilities and boundaries of standard Unix tools (`sed`, `grep`, `awk`) and Bash scripting techniques.

## Key Features

* **Bi-directional Conversion:** Seamlessly translates from `XML -> TXT` and `TXT -> XML`.
* **Stack-Based Hierarchy Tracking:** Implements a custom array-based stack (`declare -a tag_stack`) in Bash to accurately track depth and rebuild the XML tree structure from raw indented text.
* **Fail-Fast I/O Validation:** Strict file existence and extension checks before any processing begins, preventing runtime errors or corrupted outputs.
* **Interactive CLI:** A user-friendly, loop-driven terminal menu.

## Technical Limitations & Engineering Notes

This tool was built for educational purposes and is tailored for a specific, clean XML structure. It is important to note the theoretical limitations of this approach:

* **Regex vs. Context-Free Grammars:** XML is a Context-Free Grammar, meaning it cannot be perfectly parsed using Regular Expressions (`grep`/`sed`). This script works excellently on basic `<tag>value</tag>` structures but will fail on production-level XML features such as:
  * Tags with attributes (e.g., `<node id="1">`).
  * Self-closing tags (e.g., `<br/>`).
  * Multi-line nested tags or XML comments.
* **Performance:** Because Bash spawns sub-processes for every `sed` and `grep` call inside the `while` loop, processing very large XML files will be significantly slower compared to an AST-based parser written in C or Python.

## Usage

### Prerequisites
* A Unix-like environment (Linux/macOS) or WSL on Windows.
* Standard GNU tools: `bash`, `sed`, `grep`.

### Running the Script

1. Make the script executable:
   ```bash
   chmod +x parser.sh
   ```
2. Run the application:
   ```bash
   ./parser.sh
   ```
3. Follow the interactive menu to select your conversion mode and input your file names.

### Expected Formats

**Valid XML Input Example:**
```xml
<root>
    <person>
        <name>John</name>
        <age>20</age>
    </person>
</root>
```

**Valid TXT Output/Input Example:**
```text
root:
    person:
        name:
            John
        age:
            20
```
