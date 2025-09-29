# PDF OCR Parser

Modern Flask web app to extract text from PDFs using OCR only. The UI provides a drag‑and‑drop uploader, shows the extracted text, and offers Copy and Print (native PDF print dialog with page count and scaling).

## Features
- OCR‑only parsing (Tesseract) – works for scanned/image PDFs
- Clean drag‑and‑drop upload interface
- Copy extracted text in one click
- Print opens the browser’s native PDF print dialog

## Tech
- Python 3 • Flask
- Tesseract OCR via `pytesseract`
- `pdf2image` for rasterizing pages
- Frontend: vanilla HTML/CSS/JS

## Prerequisites
On Windows you’ll need the following system packages installed:

1) Tesseract OCR
- Download installer: https://github.com/UB-Mannheim/tesseract/wiki
- After install, ensure it’s on PATH (restart terminal after installing):
  ```powershell
  tesseract -v
  ```
  If not found, set the path (adjust if you installed elsewhere):
  ```powershell
  setx PATH "%PATH%;C:\\Program Files\\Tesseract-OCR"
  ```

2) Poppler (required by pdf2image)
- Easiest: install via Chocolatey
  ```powershell
  choco install poppler -y
  ```
  Or download binaries and add the `bin` folder to PATH.

Java/Tika are no longer required for normal operation since parsing is OCR‑only. The repo still includes a Tika JAR and Python deps for optional experimentation, but they are not used by default.

## Setup
```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
```

## Run
```powershell
python main.py
```
Then open `http://127.0.0.1:5000` in your browser.

## Usage
1. Drag a PDF into the dashed area or click “Choose PDF File”.
2. Wait for processing; extracted text appears below.
3. Use Copy to place text on the clipboard, or Print to open the native print dialog (choose scaling, page range, etc.).

## API
- `POST /upload` – multipart form with field `file` (PDF). Returns JSON: `{ "text": "..." }`.

## Troubleshooting
- `TesseractNotFoundError`: ensure Tesseract is installed and accessible on PATH; verify with `tesseract -v`.
- `PDFInfoNotInstalledError`: install Poppler and ensure `pdftoppm`/`pdftocairo` are on PATH.
- Very large PDFs: OCR is CPU‑intensive; try splitting the file or running with fewer pages.

## Deploying
This is a server app (Flask). Host on a Python‑friendly platform such as Render, Railway, Fly.io, or a VPS. GitHub Pages cannot run Flask.

## License
MIT

## Author
ANURAG S S

