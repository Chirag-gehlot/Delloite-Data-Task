# Deloitte Australia – Technology Job Simulation (Forage)

This repository contains my submission for **Deloitte Australia's Technology Job Simulation** on [Forage](https://www.theforage.com/). The simulation places you in the role of a Deloitte Technology Consultant, working on a data integration problem for a manufacturing client and proposing a dashboard solution for their operations team.

## 📌 Overview

The client's factories use IoT sensors from two different vendors, each reporting device data in a different JSON format. The task was to:

1. Write a Python solution that **normalizes data from both formats into a single, unified schema**, and
2. Write a **proposal for a dashboard** that the client's operations team could use to monitor factory device data.

## 🗂️ Repository Contents

| File | Description |
|---|---|
| `main.py` | Python script that converts sensor data from two different JSON formats into one unified format, with `unittest` test cases to validate the conversion logic |
| `data-1.json` | Sample input data in **Format 1** (flat structure with a slash-delimited location string) |
| `data-2.json` | Sample input data in **Format 2** (nested structure with an ISO 8601 timestamp) |
| `data-result.json` | The expected unified output format used to validate both conversions |
| `Task 3 Model Submission.docx` | Written proposal for a dashboard to visualize and monitor factory/device data |

## ⚙️ Task 1 & 2 – Data Conversion (`main.py`)

The two input formats differ in:
- **Location representation** — Format 1 stores location as a single delimited string (`country/city/area/factory/section`); Format 2 stores it as separate fields.
- **Timestamp representation** — Format 1 already uses milliseconds since epoch; Format 2 uses an ISO 8601 string that needs to be converted.
- **Data fields** — Format 1 uses `operationStatus`/`temp`; Format 2 already provides a nested `data` object.

`main.py` detects the input format (based on presence of a `device` key) and routes it to the appropriate converter:

- `convertFromFormat1()` — parses the location string and remaps status/temperature fields
- `convertFromFormat2()` — converts the ISO 8601 timestamp to epoch milliseconds and remaps nested fields

Both converters output a single unified schema:

```json
{
  "deviceID": "...",
  "deviceType": "...",
  "timestamp": 0000000000000,
  "location": {
    "country": "...",
    "city": "...",
    "area": "...",
    "factory": "...",
    "section": "..."
  },
  "data": {
    "status": "...",
    "temperature": 0
  }
}
```

### ▶️ Running the tests

```bash
python main.py
```

This runs the `unittest` suite, which checks:
- `test_sanity` — confirms the expected result file is well-formed
- `test_dataType1` — confirms Format 1 input converts correctly
- `test_dataType2` — confirms Format 2 input converts correctly

## 📊 Task 3 – Dashboard Proposal

`Task 3 Model Submission.docx` contains the written proposal recommending how the unified device data could be visualized in a dashboard for the client's operations team — covering the purpose of the dashboard, key metrics/views, and the value it would deliver to the business.

## 🎓 About This Simulation

Completed as part of **Deloitte Australia's Technology Job Simulation** on Forage, covering:
- Development and coding (data transformation logic in Python)
- Writing a technical/business proposal for a dashboard solution

## 🛠️ Tech Stack

- Python 3
- Built-in libraries: `json`, `unittest`, `datetime`

## 📄 License

This project was completed for educational purposes as part of the Forage virtual experience program.
