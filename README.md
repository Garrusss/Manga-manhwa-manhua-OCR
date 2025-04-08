# Manga-manhwa-manhua-OCR
OCR for Asian comics, working through Google Vision with a special interface tailored for comics.

# Manga OCR Tool (Google Vision)

A simple PyQt5-based desktop application for extracting text from manga/comic pages using Google Cloud Vision API. Allows users to draw bounding boxes (bubbles) around text areas, run OCR, edit the results, and export the text.

**Disclaimer:** This tool was created by a beginner primarily for personal use. Therefore, your user experience may vary. I sincerely welcome anyone who wants to help develop this project further!

## Features

*   Load PNG images.
*   Draw rectangular bubbles around text areas.
*   Differentiate between two bubble types (e.g., speech vs. thoughts/SFX), marked with `*` on export for type 2.
*   Move and resize bubbles interactively.
*   Perform OCR on the entire image using Google Cloud Vision API.
    *   Supports language hints for improved accuracy (or auto-detection).
*   Display recognized text alongside the image.
*   Edit the recognized text directly in the application.
*   Copy all extracted text (sorted by bubble number) to the clipboard.
*   Export all extracted text (sorted by bubble number) to a `.docx` file.
*   Efficient image handling using vertical strips for very tall images.
*   Saves and restores window geometry, last used directories, selected language hint, and Google Cloud key path.

## Requirements

*   Python 3.8+
*   PyQt5
*   Pillow
*   python-docx
*   google-cloud-vision
*   google-auth

## Installation

1.  **Clone or download the repository:**
    ```bash
    git clone <your-repository-url>
    cd <repository-folder>
    ```
    Or download the source code ZIP and extract it.

2.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```
    (You might need to create a `requirements.txt` file containing the libraries listed above, one per line, or install them manually: `pip install PyQt5 Pillow python-docx google-cloud-vision google-auth`)

## Google Cloud Vision API Setup (Crucial!)

This tool relies on the Google Cloud Vision API, which is a paid service (though it has a free tier). You **must** set up credentials to use it.

1.  **Create a Google Cloud Project:** If you don't have one already, create a project on the [Google Cloud Console](https://console.cloud.google.com/).
2.  **Enable the Cloud Vision API:** In your Google Cloud Project, navigate to "APIs & Services" > "Library", search for "Cloud Vision API", and enable it. You might also need to enable billing for your project, although the free tier is generous.
3.  **Create a Service Account:**
    *   Go to "APIs & Services" > "Credentials".
    *   Click "Create Credentials" > "Service account".
    *   Give it a name (e.g., "manga-ocr-tool-user").
    *   Grant it necessary permissions. The role "Cloud Vision AI Service Agent" (or potentially a more basic "Cloud Vision User") should be sufficient.
    *   Click "Done".
4.  **Generate a Key File:**
    *   Find the service account you just created in the Credentials list.
    *   Click on its email address.
    *   Go to the "KEYS" tab.
    *   Click "ADD KEY" > "Create new key".
    *   Choose "JSON" as the key type and click "CREATE".
    *   A JSON key file will be downloaded to your computer. **Keep this file secure and private!**
5.  **Provide the Key to the Application:** You have two options:
    *   **Option A (Recommended): Environment Variable**
        *   Set the environment variable `GOOGLE_APPLICATION_CREDENTIALS` to the **full path** of the downloaded JSON key file. The application will automatically detect and use it.
        *   How to set environment variables depends on your operating system (Windows, macOS, Linux). Search online for instructions specific to your OS.
    *   **Option B: In-App Setting**
        *   Run the application.
        *   Go to the "File" menu > "Set Google Cloud Key...".
        *   Browse and select the downloaded JSON key file.
        *   The application will save the path to this file in its settings and use it for future OCR requests.

## Usage

1.  **Run the application:**
    ```bash
    python OCR.py
    ```
    (Make sure `OCR.py` is the correct name of your main script file).

2.  **Open Image(s):** Use "File" > "Open PNG..." or the folder icon to load one or more PNG files. Each image will open in a new tab.
3.  **Select Bubble Type:** Click the "Type 1" or "Type 2" button on the toolbar to activate drawing mode for that type. Click the active button again to deactivate drawing mode and return to panning/selection.
4.  **Draw Bubbles:** While in drawing mode (crosshair cursor), click and drag on the image to draw rectangles around text areas.
5.  **Adjust Bubbles:** Click on a bubble to select it. You can then move it by dragging or resize it using the handle in the bottom-right corner. Right-click on a bubble for more options (change type, delete, trigger OCR).
6.  **Run OCR:** Click the "Scan All Bubbles" button (play icon) or right-click a bubble and choose "Recognize Text (OCR)". This sends the *entire* image to Google Vision.
7.  **View/Edit Text:** The recognized text will appear in the text panel on the right, sorted by bubble number. You can edit the text directly in this panel. Edits are saved automatically to the corresponding bubble.
8.  **Copy/Export:** Use the "Copy Text" button or "Edit" > "Copy Text" to copy the content to the clipboard. Use the "Export to DOCX" button or "Edit" > "Export to DOCX..." to save the content as a Word file. Type 2 bubbles will have a `* ` prefix in the copied/exported text.

## Contributing

As mentioned, this is a beginner's project. Contributions are very welcome! Feel free to:

*   Open an Issue to report bugs or suggest features.
*   Fork the repository and submit a Pull Request with improvements or fixes.
