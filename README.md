# 🧪 IT3040 – ITPM Assignment 1
## Transliteration Accuracy Testing — Chat Sinhala (Singlish → Sinhala)

### Student Information

| Field | Details |
|---|---|
| **Student Name** | BHANUKA H.M.V |
| **Registration Number** | IT23842076 |
| **Module** | IT3040 – IT Project Management |
| **Year / Semester** | Year 3 / Semester 1 |
| **Assignment** | Assignment 1 — Option 1 |
| **Institution** | Sri Lanka Institute of Information Technology (SLIIT) |
| **Program** | BSc (Hons) in Information Technology |

---

## 📌 Project Overview

This project automates the functional testing of the **Chat Sinhala transliteration** feature available at:

🔗 [https://www.pixelssuite.com/chat-translator](https://www.pixelssuite.com/chat-translator)

### Project Objective

The automation framework identifies and validates **negative test cases** where the Chat Sinhala system fails to correctly convert Singlish (chat-style romanized Sinhala) input into proper Sinhala output. This comprehensive test suite covers **50 negative test cases** spanning **24 different Singlish input types** as defined in Appendix 1 of the assignment specification.

### Key Testing Scope

- **Test Count**: 50 negative test cases
- **Input Type Coverage**: 24 distinct Singlish input types
- **Platform**: Web-based Chat Translator (Playwright automation)
- **Output Validation**: Automatic comparison of actual vs. expected Sinhala output
- **Result Logging**: Real-time results captured in Excel spreadsheet

---

## 📁 Project Structure

```
test_automation/
│
├── test_automation.py                              # Main Playwright automation script
├── Assignment 1 - Test cases_results_results_results.xlsx   # Excel file with test cases & results
└── README.md                                       # This documentation file
```

### File Descriptions

#### test_automation.py
The primary automation script that:
- Loads test cases from Excel
- Auto-detects header row and column mappings
- Launches Chrome/Chromium browser via Playwright
- Navigates to the Chat Translator URL
- Inputs Singlish text and captures Sinhala output
- Compares output against expected values
- Updates Excel with actual output and test status
- Implements retry logic for unstable UI responses
- Supports save checkpoints during execution

#### Assignment 1 - Test cases_results_results_results.xlsx
The Excel workbook containing:
- **Input Column**: Singlish test inputs
- **Expected Output Column**: Expected Sinhala translations
- **Actual Output Column**: Populated by automation script
- **Status Column**: Test result (PASS/FAIL/COLLECTED/UI Error)
- **Header Row**: Auto-detected or manually specified
- **Sheet Format**: Compatible with merged cells and flexible column naming

---

## ✅ System Prerequisites

Before running the tests, ensure your system has the following installed:

### Required Software
- **Python**: Version 3.10 or higher (3.12.10 recommended)
- **Browser**: Google Chrome, Chromium, or Firefox
- **Node.js/npm**: Optional (for advanced Playwright features)
- **Git**: Optional (for version control)

### Required Python Packages
- **playwright** (≥ 1.40.0) — Browser automation
- **openpyxl** (≥ 3.0.0) — Excel file handling

---

## ⚙️ Detailed Setup Instructions

### Step 1: Download and Extract Project

1. Download the project ZIP file
2. Extract to your preferred location (e.g., `D:\test_automation` or `C:\Users\YourUsername\Downloads\test_automation`)
3. The folder should contain:
   - `test_automation.py`
   - `Assignment 1 - Test cases_results_results_results.xlsx`
   - `README.md`

### Step 2: Open Command Prompt or PowerShell

**Option A: Command Prompt**
- Press `Win + R`
- Type `cmd` and press Enter

**Option B: PowerShell**
- Right-click on the project folder
- Select "Open PowerShell window here"

### Step 3: Navigate to Project Folder

```bash
cd /d C:\Users\it23842076\Downloads\test_automation
```

> Note: Adjust the path based on where you extracted the project

### Step 4: Create Virtual Environment (Recommended)

```bash
python -m venv venv
```

Activate the virtual environment:

**On Windows (Command Prompt):**
```bash
venv\Scripts\activate
```

**On Windows (PowerShell):**
```bash
venv\Scripts\Activate.ps1
```

### Step 5: Upgrade pip

```bash
python -m pip install -U pip
```

### Step 6: Install Required Python Packages

```bash
pip install playwright openpyxl
```

### Step 7: Install Playwright Browser Binaries

```bash
playwright install chromium
```

Or for all browsers:
```bash
playwright install
```

---

## ▶️ Running the Test Automation

### Basic Execution

Once all dependencies are installed, execute the script with:

```bash
python test_automation.py
```

### Recommended Execution (with all options)

```bash
python test_automation.py ^
  --excel "Assignment 1 - Test cases_results_results_results.xlsx" ^
  --url "https://www.pixelssuite.com/chat-translator" ^
  --wait-ms 5000 ^
  --type-delay-ms 80 ^
  --slow-mo-ms 200 ^
  --save-every 1 ^
  --keep-open
```

> Note: On PowerShell, replace `^` with a backtick `` ` ``

### Execution Flow

1. **Initialization**: Script loads Excel file and detects header row
2. **Browser Launch**: Opens Chrome/Chromium in visible mode
3. **Page Load**: Navigates to Chat Translator URL
4. **Iteration**: For each test case:
   - Dismisses any overlay dialogs
   - Clears the input textarea
   - Types Singlish input with specified delay
   - Clicks "Transliterate" button
   - Waits for output with retry logic
   - Captures Sinhala output
   - Compares with expected value
   - Updates Excel with result
5. **Completion**: Saves workbook and closes browser (unless `--keep-open` is set)

---

## 🔧 Command-Line Arguments Reference

| Argument | Type | Default | Description |
|---|---|---|---|
| `--excel` | path | Auto-detected | Path to Excel test case file |
| `--sheet` | string | Auto-detected | Sheet name containing test cases |
| `--header-row` | integer | Auto-detected | Row number containing column headers (1-based) |
| `--max-header-scan-rows` | integer | 30 | Maximum rows to scan for header detection |
| `--input-col` | string | Auto-detected | Column name for Singlish input |
| `--expected-col` | string | Auto-detected | Column name for expected Sinhala output |
| `--actual-col` | string | "Actual output" | Column name for captured output |
| `--status-col` | string | "Status" | Column name for test status |
| `--url` | URL | https://www.pixelssuite.com/chat-translator | Target website URL |
| `--output` | path | Same as input | Output Excel file path |
| `--save-every` | integer | 0 | Save results after every N test cases (0 = only at end) |
| `--headless` | flag | false | Run browser in headless mode (invisible) |
| `--wait-ms` | integer | 5000 | Milliseconds to wait after submitting input |
| `--retries` | integer | 8 | Number of times to retry reading output |
| `--retry-wait-ms` | integer | 1000 | Milliseconds to wait between retries |
| `--type-delay-ms` | integer | 30 | Milliseconds delay between keystrokes |
| `--timeout-ms` | integer | 60000 | Playwright global timeout in milliseconds |
| `--slow-mo-ms` | integer | 0 | Slow down all Playwright actions (0 = no delay) |
| `--keep-open` | flag | false | Keep browser open after test completion |

### Argument Examples

**Quick Test (Fast Execution):**
```bash
python test_automation.py --headless --wait-ms 2000 --type-delay-ms 0
```

**Detailed Test (Watch Every Step):**
```bash
python test_automation.py --slow-mo-ms 500 --type-delay-ms 100 --wait-ms 8000
```

**Save Checkpoints:**
```bash
python test_automation.py --save-every 5
```
Saves results after every 5 test cases, allowing recovery if interrupted.

---

## 📊 Results and Output

### Result File Location

After execution completes:
```
C:\Users\it23842076\Downloads\test_automation\Assignment 1 - Test cases_results_results_results.xlsx
```

### Excel Output Columns

**Automatic Columns Created/Updated:**

- **Actual output**: Contains the Sinhala text captured from the translator
- **Status**: Contains the test result status (see below)

### Status Values Explained

| Status | Meaning | When It Occurs |
|---|---|---|
| **PASS** | ✅ Test Passed | Actual output exactly matches expected output |
| **FAIL** | ❌ Test Failed | Actual output differs from expected output |
| **COLLECTED** | 📝 Data Collected | Expected output was empty, actual output captured for review |
| **UI Error** | ⚠️ Interaction Error | Browser automation encountered an error during interaction |

### Reading the Results

1. Open `Assignment 1 - Test cases_results_results_results.xlsx` in Excel
2. Locate the "Actual output" column — contains translated Sinhala text
3. Locate the "Status" column — shows PASS/FAIL/COLLECTED/UI Error
4. Analyze failed cases for patterns in what types of inputs fail
5. Generate test report based on failure distribution across input types

---

## 🗂️ Test Case Coverage Details

### Input Type Categories (24 Total)

The 50 test cases are distributed across these 24 Singlish input types:

| # | Input Type | Example | Purpose |
|---|---|---|---|
| 1 | Question forms | "oyage nam koii daa?" | Interrogative sentences |
| 2 | Command forms | "plis help me" | Imperative/command structures |
| 3 | Greetings | "hallo anna" | Greeting expressions |
| 4 | Requests | "can u hlp me" | Polite requests |
| 5 | Responses | "ok sure" | Response patterns |
| 6 | Repeated Words | "hllo hllo" | Word repetition |
| 7 | Punctuation Marks | "hello... ok!" | Special punctuation handling |
| 8 | Romanization Variants | "sinhala/sinhla/sinhal" | Spelling variations |
| 9 | Isolated English Words | "hello maam" | Single English words in Singlish |
| 10 | English Phrases | "good morning anna" | Multi-word English phrases |
| 11 | Digital Terms | "wifi connect", "5G network" | Technology/digital terms |
| 12 | Platform/App Names | "facebook message", "whatsapp group" | App/platform names |
| 13 | Abbreviations | "asap", "msg", "pls" | Abbreviated forms |
| 14 | Clipped Forms | "bro", "sis", "koko" | Informal clipped words |
| 15 | Place Names | "colombo", "kandy", "galle" | Geographic locations |
| 16 | Person Names | "john", "susan", "ramesh" | Personal names |
| 17 | Numbers & Suffixes | "123", "2nd place", "5 times" | Numeric input |
| 18 | Currency | "50 rs", "$100", "1000 rupees" | Money/currency format |
| 19 | Time Formats | "3:30 pm", "14:45", "morning 8 o'clock" | Time expressions |
| 20 | Dates | "12/05/2024", "25 may", "next monday" | Date expressions |
| 21 | Measurements | "5 kg", "10 meters", "2 hours" | Units of measurement |
| 22 | Slang/Casual | "yo sup", "wassup bro", "see u l8r" | Casual/slang speech |
| 23 | Online Identifiers | "@user", "#hashtag", "email@domain.com" | Web identifiers |
| 24 | Emojis | "hello 😊", "great! 👍", "sad 😢" | Emoji handling |

### Test Case Distribution

- **Total Negative Test Cases**: 50
- **Input Types Covered**: 24
- **Minimum Cases per Type**: 2
- **Test Case ID Format**: `Neg_XXXX` (where XXXX is the test number)

---

## 🔍 Troubleshooting Guide

### Issue 1: Module Not Found Error
```
ModuleNotFoundError: No module named 'playwright'
```
**Solution:**
```bash
pip install playwright
```

### Issue 2: Browser Launch Fails
```
Error: Could not find Chromium/Chrome
```
**Solution:**
```bash
playwright install chromium
```
Or install all browser binaries:
```bash
playwright install
```

### Issue 3: Excel File Lock Error
```
PermissionError: [Errno 13] Permission denied
```
**Solution:**
- Close the Excel file in Microsoft Excel
- Or the script will auto-save to a fallback filename with `_results` suffix
- Check your Downloads folder for alternate output file

### Issue 4: "Could not find Chat UI locators"
```
RuntimeError: Could not find Chat UI locators (input/output textareas)
```
**Causes & Solutions:**
- **Page not loaded**: Increase `--wait-ms` to 8000 or higher
- **URL incorrect**: Verify `--url` parameter points to chat-translator
- **Page structure changed**: Website may have been updated
- **Overlays blocking**: Dismiss cookie/privacy consent popups manually

**Debug Steps:**
```bash
python test_automation.py --url "https://www.pixelssuite.com/chat-translator" --slow-mo-ms 1000
```
Watch the browser and identify where it fails.

### Issue 5: Slow Execution / Timeout
```
TimeoutError: Timeout 60000ms exceeded
```
**Solutions:**
- Increase `--timeout-ms` to 120000 (2 minutes)
- Increase `--wait-ms` to 8000
- Check internet connection speed
- Reduce `--save-every` to improve performance

### Issue 6: Column Not Found
```
Error: Could not resolve input column
```
**Solutions:**
1. Check Excel file structure — verify column headers exist
2. Use explicit column names:
   ```bash
   python test_automation.py --input-col "Singlish" --expected-col "Sinhala"
   ```
3. Specify header row manually:
   ```bash
   python test_automation.py --header-row 1
   ```

### Issue 7: All Tests Show "UI Error"
**Likely Causes:**
- Website structure changed
- Network connectivity issues
- Browser not properly initialized

**Debug Steps:**
```bash
python test_automation.py --headless false --slow-mo-ms 1000 --keep-open
```
Inspect what's happening in the browser window.

---

## 💡 Advanced Usage Tips

### Running a Subset of Tests

Edit the Excel file:
1. Delete rows you don't want to test
2. Save the file
3. Run the script normally

### Collecting Data Without Expected Values

If you only want to capture output without comparing:
- Leave the "Expected output" column empty
- Status will show "COLLECTED" for all entries
- This allows data collection for future analysis

### Batch Testing Multiple Excel Files

Create a batch script (`run_tests.bat`):
```batch
@echo off
python test_automation.py --excel "Test_Set_1.xlsx"
python test_automation.py --excel "Test_Set_2.xlsx"
python test_automation.py --excel "Test_Set_3.xlsx"
echo All tests completed!
pause
```

Run with:
```bash
run_tests.bat
```

### Logging to File

Capture all output to a log file:
```bash
python test_automation.py > test_results.log 2>&1
```

---

## 📋 Pre-Execution Checklist

Before running the automation, verify:

- [ ] Python 3.10+ is installed: `python --version`
- [ ] Playwright is installed: `pip list | findstr playwright`
- [ ] openpyxl is installed: `pip list | findstr openpyxl`
- [ ] Excel file path is correct and file is not open
- [ ] Internet connection is stable
- [ ] Target URL is accessible in your browser
- [ ] Chrome/Chromium browser is installed
- [ ] No antivirus blocking Playwright processes
- [ ] Sufficient disk space for browser cache

---

## 📈 Expected Results Summary

### Success Indicators

✅ Script completes without errors  
✅ Browser closes gracefully  
✅ Excel file updated with results  
✅ Status column populated for all rows  
✅ Actual output column contains Sinhala text  

### Performance Metrics

- **Typical Execution Time**: 5-10 minutes for 50 test cases
- **Per-Test Time**: ~6-12 seconds per test case
- **Network Dependency**: High (depends on Chat Translator responsiveness)

---

## 📚 Test Case Analysis Framework

### Failure Analysis

After execution, analyze failed cases:

1. **Identify Patterns**: Which input types have highest failure rates?
2. **Categorize Failures**: 
   - Translation errors
   - Special character handling
   - Mixed language processing
   - Emoji/symbol issues
3. **Document Findings**: Create test report with:
   - Total tests: 50
   - Pass count
   - Fail count
   - Error count
   - Pass rate percentage

### Sample Analysis Report Format

| Input Type | Tests | Passed | Failed | Pass Rate |
|---|---|---|---|---|
| Question forms | 2 | 2 | 0 | 100% |
| Command forms | 2 | 1 | 1 | 50% |
| ... | ... | ... | ... | ... |
| **TOTAL** | **50** | **XX** | **YY** | **XX%** |

---

## 📞 Support & Contact

For issues or questions:
1. Review the Troubleshooting section above
2. Check the Playwright documentation: https://playwright.dev/python/
3. Check openpyxl documentation: https://openpyxl.readthedocs.io/

---

## 📄 Assignment Submission Files

Your submission should include:
```
test_automation/
├── test_automation.py
├── Assignment 1 - Test cases_results_results_results.xlsx
├── README.md
└── [Test Analysis Report] (optional but recommended)
```

---

**Last Updated**: May 4, 2026  
**Program**: BSc (Hons) in Information Technology  
**Institution**: Sri Lanka Institute of Information Technology (SLIIT)  
**Year 3 | Semester 1**
