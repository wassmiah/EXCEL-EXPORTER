# WF Excel Exporter

Windows tool for exporting every **visible** Google Sheets tab as a separate `.xlsx` file.

## What it does

For every visible tab:

1. Reads the tab's current calculated values from the Google Sheets API.
2. Downloads the tab with the same Google `export?format=xlsx&gid=...` method used in the browser.
3. On the PC, replaces exported formula cells with the values currently calculated by Google Sheets.
4. Removes Excel data-validation/dropdown rules.
5. Saves `<SHEET NAME>.xlsx` locally.

It does **not** create temporary Google Sheets, temporary tabs, or Drive copies.

The XLSX is patched at XML level, so the rest of the downloaded Excel package is left intact as much as possible: styles, number formats, merged cells, borders, widths/heights, drawings, print settings, etc.

## One-time Google setup

You need a Google OAuth **Desktop app** credentials JSON file.

1. Open Google Cloud Console.
2. Create/select a project.
3. Enable **Google Sheets API** and **Google Drive API**.
4. Configure the OAuth consent screen.
5. Create an OAuth Client ID with application type **Desktop app**.
6. Download the client JSON file.
7. In the exporter, browse to that JSON file.

The first export opens your browser for Google sign-in. The resulting token is stored locally at:

`%APPDATA%\WFExcelExporter\token.json`

Use **Reset Google Login** in the app if you need to sign in with a different Google account.

## Install

1. Install Python 3.11 or newer for Windows.
2. Extract this project folder.
3. Double-click `setup.bat` once.
4. Double-click `run.bat`.

## Use

1. Paste your Google Sheets URL, for example:

   `https://docs.google.com/spreadsheets/d/YOUR_FILE_ID/edit`

2. Select your OAuth `credentials.json`.
3. Select the output folder.
4. Click **Export Visible Sheets**.

A dated output folder is created automatically. Hidden tabs are skipped.

## Optional EXE

After `setup.bat` succeeds, double-click `build_exe.bat`.

The packaged application will be created under:

`dist\WF Excel Exporter.exe`

Keep your OAuth credentials JSON outside the EXE and select it in the app.

## Important

The Google account used in the OAuth browser sign-in must have access to the spreadsheet and permission to download/export it.
