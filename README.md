# OnePagerScript

A Google Ads Script to automate the consolidation and reporting of campaign, item ID, and PMax placement data into a central Google Sheets dashboard. This script is designed for PPC managers and analysts who want to streamline their data pulls and comparisons, merging results from the Google Ads API and a separate PMax placement output.

---

## Features

- **Campaign Performance Dump:** Pulls campaign-level performance for a configurable date range, with previous period comparison.
- **Item ID Performance Dump:** Pulls item-level (product) performance with period-over-period metrics.
- **PMax Placement Import:** Imports PMax placement data from a separate Google Sheet into your main report.
- **Automated Sheet Management:** Clears previous data (but keeps headers) before writing new data.
- **Error Logging:** Extensive logs for easier debugging.

---

## Prerequisites

- Access to [Google Ads Scripts](https://ads.google.com/aw/scripts/).
- Two Google Sheets:
  - **Main Reporting Spreadsheet** (where this script writes all outputs).
  - **PMax Placement Data Spreadsheet** (where your other script outputs PMax placement data).
- Editor access to both Sheets and the ability to configure Google Ads accounts.
- You must have another script/output that writes PMax placement data to the second spreadsheet.

---

## Setup Guide

### 1. Prepare Your Google Sheets

**a) Main Reporting Spreadsheet**

- Create a new Google Sheet (or use an existing one).
- Add the following tabs (sheet names must match exactly):
  - `Campaign Performance Dump`
  - `item-id Dump`
  - `PMAX Placements Dump`
- Add appropriate header rows (row 1) to each tab. The script does **not** auto-create headers.

**b) PMax Placement Data Spreadsheet**

- This sheet is where your separate PMax placement script writes data.
- Note the spreadsheet URL and the name of the tab containing placement data (e.g. `Campaigns`).

---

### 2. Configure the Script

Open [Google Ads Scripts](https://ads.google.com/aw/scripts/) and create a new script.

Replace the contents with the code from this repository.

**In the script, configure the following variables at the top of the `main()` function:**

```js
// 1. Main reporting spreadsheet URL:
const SPREADSHEET_URL = 'YOUR_ONEPAGER_URL_SHEET'; // <-- Replace with your actual Google Sheet URL

// 2. PMax Placement source spreadsheet URL:
const SOURCE_PMAX_SPREADSHEET_URL = 'URL_OF_PMAXSCRIPT_OUTPUT_SPREADSHEET_HERE'; // <-- Replace with the actual URL

// 3. Name of the tab in the source PMax spreadsheet:
const SOURCE_PMAX_SHEET_NAME = 'Campaigns';

// 4. Date range for reporting (choose 91 or 365 only):
const NUMBER_OF_DAYS = 91; // or 365
```

**_Tip:_**  
If you create new tabs in your main spreadsheet, ensure the tab names in the script (`CAMPAIGN_SHEET_NAME`, `ITEM_ID_SHEET_NAME`, `PMAX_PLACEMENT_DUMP_SHEET_NAME`) match your tabs exactly.

---

### 3. Grant Permissions

- When you run the script for the first time, Google will ask for authorization to access your Google Ads and Google Sheets accounts.
- Approve the required permissions.

---

### 4. Run the Script

1. In Google Ads Scripts, press the **"Preview"** button to test.
2. Check the logs for errors and ensure data is written to your main spreadsheet as expected.
3. Once satisfied, schedule the script or run it as needed.

---

## Sheet/Tab Structure

**Campaign Performance Dump**  
Headers should include (example):  
`Campaign Name, Status, Channel, Network, Impressions, Last Period Impressions, Clicks, Last Period Clicks, Cost, Last Period Cost, Conversions, Last Period Conversions, Conv. Value, Last Period Conv. Value`

**item-id Dump**  
Headers should include:  
`Item ID, Impressions, Last Period Impressions, Clicks, Last Period Clicks, Cost, Last Period Cost, Conversions, Last Period Conversions, Total conversion value, Last Period Total conversion value`

**PMAX Placements Dump**  
- Headers must match the columns in your source placement data.
- Data will be written starting from row 2.

---

## Troubleshooting

- **Sheet not found?**  
  The script will auto-create any missing tabs, but you must add headers manually.

- **Data not updating?**  
  Make sure the URLs and sheet names in the script match your actual sheets/tabs.

- **Authorization errors?**  
  Re-run the script and re-authorize as needed.

- **No data for a period?**  
  Check your date range and your Google Ads account permissions.

- **PMax placement import fails?**  
  Confirm the source spreadsheet is accessible, and the tab name is correct.

- **Headers erased?**  
  The script only clears data below the header (row 2 and down), but if you change tab names or structure, you may need to restore headers.

---

## Customization

- You can adjust the field selections in the GAQL queries in the functions for campaign and item ID data.
- The script is modular; feel free to add additional dumps or modify as needed.
- For advanced users: you may wish to move `formatDateForGAQL` to global scope if calling sub-functions standalone.

---

## License

MIT License

---

## Author

[https://github.com/XeonIsh](https://github.com/XeonIsh)
