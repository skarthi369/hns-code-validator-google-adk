# HSN Code Validation Agent

This agent validates Harmonized System Nomenclature (HSN) codes using a master dataset in Excel format. It checks if the codes are correctly formatted, exist in the master data, and (optionally) if parent codes exist for 8-digit codes.

---

## Features

- **Input Handling:** Accepts single or multiple HSN codes (comma, space, or semicolon separated).
- **Format Validation:** Ensures codes are numeric and of valid lengths (2, 4, 6, or 8 digits).
- **Existence Validation:** Checks if the code exists in the master dataset.
- **Hierarchical Validation:** For 8-digit codes, checks if parent codes (first 2, 4, 6 digits) exist.
- **Conversational:** Provides clear, user-friendly responses via the Google ADK framework.

---

## Architecture

User Input (HSN codes)|v[HSN Code Validation Agent (agent.py)]||-- Loads HSN master data from Excel (HSN_SAC.xlsx)|-- Utilizes validate_hsn_codes tool|-- Validates format, existence, and hierarchyvAgent Response (valid/invalid, description, reasons)
- The agent is implemented in `agent.py` (or your main agent script) using the Google Agent Development Kit (ADK).
- The master data is loaded from an Excel file (e.g., `HSN_SAC.xlsx`). The script expects the first column to contain HSN codes and the second column to contain their descriptions.
- The agent exposes a tool for code validation and is accessible via the ADK web interface or CLI.

---

## Requirements

- Python 3.7+
- `pandas`
- `openpyxl`
- Google Agent Development Kit (ADK)

---

## Setup

1.  **Install dependencies:**
    Create a `requirements.txt` file in your project directory:
    ```txt
    google-adk
    pandas
    openpyxl
    ```
    Then install them:
    ```sh
    pip install -r requirements.txt
    ```
    *(Ensure you have also installed the Google Agent Development Kit (ADK) itself as per its official documentation if it's not covered by `pip install google-adk` for all necessary components like the CLI.)*

2.  **Place your HSN master Excel file:**
    * Ensure your HSN master data Excel file (e.g., `HSN_SAC.xlsx`) is accessible.
    * Update the `HSN_MASTER_FILE` variable in your agent script (`agent.py`) to point to the correct path of this file. For example:
        ```python
        HSN_MASTER_FILE = r"C:\Users\skarthi\Downloads\agent-development-kit-crash-course-main\agent-development-kit-crash-course-main\1-basic-agent\greeting_agent\HSN_SAC.xlsx"
        # Or a relative path if the file is within your project structure:
        # HSN_MASTER_FILE = "data/HSN_SAC.xlsx"
        ```
    * The Excel file's **first column** should contain HSN codes, and the **second column** should contain their descriptions.

---

## How to Run

1.  **Activate your virtual environment** (if using one):
    * Windows PowerShell:
        ```sh
        .venv\Scripts\Activate.ps1
        ```
    * Windows CMD:
        ```sh
        .venv\Scripts\activate.bat
        ```
    * macOS/Linux:
        ```sh
        source .venv/bin/activate
        ```

2.  **Navigate to the project directory:**
    Open your terminal. The `adk web` or `adk run` commands are typically run from the parent directory of your agent module. For example, if your agent code is in a folder named `my_hsn_agent_module`, you would navigate to the directory containing `my_hsn_agent_module`.
    ```sh
    cd /path/to/your/project_root # This directory should contain your agent module folder
    ```
    If your agent script is directly in `1-basic-agent/greeting_agent` and this folder itself is the agent module recognized by ADK, you might `cd` into `1-basic-agent` or its parent, depending on how ADK discovers agents. The example `cd 1-basic-agent/greeting_agent` followed by `adk web` implies ADK can run from within the agent's directory or a specific project structure. Refer to ADK documentation for precise discovery rules.

3.  **Run the ADK web server or CLI:**
    * To run with the development web UI:
        ```sh
        adk web <your_agent_module_name>
        # Example: If your agent module folder is 'hsn_validator_module'
        # adk web hsn_validator_module
        # If running from within the agent module folder itself, 'adk web' might suffice
        # if ADK auto-detects it.
        ```
    * To run with the command-line interface:
        ```sh
        adk run <your_agent_module_name>
        ```

4.  **Open your browser** (if using `adk web`) and go to the address shown in the terminal (usually `http://localhost:8000`).

5.  **Interact with the agent** by providing HSN codes for validation as per the agent's instructions.

---

## Usage Example

**User Input:**
Validate the following HSN codes: 01011010, 123456, 0101, 99999999.
**Conceptual Agent Output (will vary based on your HSN data and agent's conversational style):**
Okay, I can help with that! Here are the validation results:HSN Code 01011010: This code is valid. Description: [Description for 01011010 from your HSN_SAC.xlsx].HSN Code 123456: This code was not found in the master data.HSN Code 0101: This code is valid. Description: [Description for 0101 from your HSN_SAC.xlsx].HSN Code 99999999: This code was not found in the master data.
---

## Configuration

-   The primary configuration is the `HSN_MASTER_FILE` variable in your agent script (`agent.py`). Ensure this path correctly points to your HSN master data Excel file.

---

## Troubleshooting

-   **File Not Found Error for `HSN_SAC.xlsx`:**
    Ensure the Excel file exists at the path specified in the `HSN_MASTER_FILE` variable within your agent script. Double-check the filename and the full path.
-   **Missing Dependency (e.g., `ImportError: Missing optional dependency 'openpyxl'`):**
    If you encounter errors about missing libraries like `openpyxl` (even if pandas is installed), install it explicitly:
    ```sh
    pip install openpyxl
    ```
    Ensure all dependencies from `requirements.txt` are installed in your active Python environment.
-   **ADK Command Not Found:**
    Make sure the Google Agent Development Kit is correctly installed and its CLI tools (`adk`) are in your system's PATH. You might need to reactivate your virtual environment or check your ADK installation.

-----------------------------------------------------------------------------------------------------------------------
