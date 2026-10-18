# HTML Loader

A lightweight, single-file HTML loader and document preview tool built with HTML, CSS, and JavaScript. Load local files, fetch remote URLs, generate Blob and Data URLs, preview documents, and export the loader itself — all from one webpage.

**No installation, build tools, frameworks, or dependencies are required.**

## Features

- **Single-file application:** The entire loader runs from one HTML file.
- **Local file loading:** Select a file using the file picker or drag and drop it onto the page.
- **Remote URL loading:** Fetch files from URLs when the server permits cross-origin requests.
- **Multiple loading methods:** Open files using Blob URLs, Data URLs, a new tab, an iframe, or an object element.
- **Content-aware previews:** Display images, HTML, text, PDFs, and other files using different preview methods.
- **File metadata:** Inspect a file's name, MIME type, size, and last-modified date.
- **Fullscreen preview:** Expand the preview area to fill the screen.
- **File System Access API:** Use the browser's native file picker where supported.
- **Clipboard tools:** Copy the generated Data URL or the loader's raw HTML source.
- **Download and export:** Download a copy of the loader as an HTML file.
- **Dark interface:** A dark-themed UI designed for convenient use.

## Getting Started

### Option 1: Download and run locally

1. Download `loader.html` from this repository.
2. Open it in a modern browser such as Chrome, Firefox, or Edge.
3. Select a local file or drag and drop one onto the page.
4. Choose a loading method to open or preview the file.
### Option 2: There is no option 2!
Sorry, but GitHub Pages site isn't up yet, and honestly, I'm pretty lazy so it will probably never happen.

## How to Use

### 1. Load a file

There are two main ways to provide a file.

**Select a local file**

Click the file picker and choose a file. The loader reads its contents and displays basic information about the selected file.

**Drag and drop**

Drag a file onto the webpage. A drop overlay appears while dragging; release the file to load it.

The file input is configured to accept HTML and plain-text files, but drag-and-drop and other loading methods may accept additional file types.

### 2. Load a remote file

Enter a file URL into the remote URL field and click **Load from URL**.

The loader attempts to fetch the resource, read its contents, and make it available to the other loading methods.

**Important:** Remote fetching depends on CORS (Cross-Origin Resource Sharing). A website must permit your page's origin to read its response. A URL opening successfully in a browser does not necessarily mean JavaScript can fetch it.

### 3. Choose a loading method

| Button | What it does | Important notes |
|---|---|---|
| **Open as blob link** | Creates a temporary Blob URL for the loaded file. | Useful for opening file content without embedding all its bytes in a URL. |
| **Open as text link** | Creates a Data URL from the file's contents. | Can consume substantial memory for large files. |
| **Open in blank page** | Writes the loaded text into a newly opened browser tab. | Popup blocking may prevent it from opening. Reloading the new tab does not preserve the generated document. |
| **Load into box** | Displays the file's text inside an iframe using `srcdoc`. | Intended primarily for HTML content. |
| **`<object>`** | Loads the selected file through an object element and a Blob URL. | Browser support and rendering behavior vary by file type. |
| **Load into page** | Displays the loaded content as text in the preview area. | This does not execute or render the HTML as a webpage. |
| **Revoke Blob:URL** | Releases the currently tracked Blob URL. | A revoked URL can no longer be used to access its Blob. |
| **Fullscreen** | Toggles fullscreen mode for the preview container. | The browser may require a user interaction or permission. |
| **File System Access API** | Opens the browser's native file picker and reads the selected file. | Requires a supporting browser; this implementation reads the file into memory. |
| **Weird file types button** | Attempts to choose a preview based on the file type or extension. | Images, PDFs, HTML, and text receive specialized previews; other formats use the object element. |
| **Clear page** | Clears the selected file and current preview. | Use this before selecting another file with the same name if the current file input does not register the selection again. |

### 4. Configure the toggles

- **Open URL in new tab:** Automatically opens generated Blob or Data URLs in a new tab. Enabled by default.
- **Copy URL to clipboard:** Copies a generated URL instead of displaying it in the output area. Clipboard permissions may affect this feature.
- **Show file metadata:** Displays the selected file's name, MIME type, size, and last-modified date.
- **Auto-preview (Content Aware):** Automatically attempts to preview a selected local file according to its detected type or filename extension.

Hover over the buttons for additional descriptions.

### 5. Keyboard shortcuts

| Key | Action |
|---|---|
| Backtick (`) | Clears the current page and preview. |
| Tilde (~) | Attempts to close the browser tab. This may not work for tabs opened manually. |

### 6. Export the loader

At the bottom of the page, you can use these buttons:

- **Download Webpage:** Downloads the current loader as `loader.html`.
- **Copy Data:URL:** Copies a Base64-encoded Data URL containing the loader's HTML.
- **Copy Raw HTML:** Copies the loader's HTML source to the clipboard.

Large Data URLs can become impractical to copy, share, or open. Clipboard access may also require a secure context or browser permission.

## Supported File Types

Support depends on the browser and the actual contents of the file.

| File type | Expected behavior |
|---|---|
| HTML / HTM | Render through an iframe or another HTML-capable loading method. |
| TXT and other text files | Display as text. |
| JSON / XML | Display as text when recognized by the content-aware preview. |
| Images | Display in the image preview when the MIME type is recognized. |
| PDF | Attempt to display through an object element. |
| Other formats | Attempt an object-element preview; support varies. |

This is not a universal document converter. Formats such as RTF, MP4, and other binary documents may not display correctly in every browser. Some formats require a dedicated viewer or additional processing.

## Privacy and Security

- Local file selection is handled by the browser; the loader does not intentionally upload local files to a server.
- Remote URL loading makes a network request to the specified URL.
- HTML loaded into an iframe, object element, or new tab may contain scripts or other active content.
- Only load files and URLs you trust. Untrusted HTML can execute JavaScript and potentially interact with browser-accessible resources, depending on its execution context and security restrictions.
- Blob URLs are temporary and are intended for use within the browser context that created them.
- The File System Access API is browser-controlled; this implementation reads the chosen file rather than implementing a general-purpose file editor.

**Tip:** Use a separate browser profile or an appropriately isolated environment when testing untrusted HTML.

## Known Limitations

- Remote fetching may fail because of CORS, authentication, network errors, or server restrictions.
- Browser popup blockers can prevent new tabs from opening.
- Data URLs can become extremely large and slow to process.
- File rendering varies across browsers and operating systems.
- The File System Access API is not supported in every browser.
- Some metadata or MIME types may be missing or inaccurate.
- The current implementation has limited handling for selecting the same file repeatedly.
- The content-aware preview is a basic file-type selector, not a complete file-format detection engine.

## Roadmap

Potential future improvements:

- Add an optional CORS-compatible remote-fetching solution.
- Add more document preview methods.
- Improve same-file reselection and state management.
- Improve error messages and loading feedback.
- Expand content-aware format detection.
- Improve large-file handling and memory usage.
- Refine clipboard and export behavior.

## Technologies

- HTML5
- CSS3
- Vanilla JavaScript
- File API and FileReader
- Blob URLs and Data URLs
- Fetch API
- iframe and object elements
- Fullscreen API
- File System Access API, where supported

No package manager or build process is needed.

## License

This project is licensed under the **Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0)** license.

You may share and adapt the project, including for commercial purposes, provided you follow the license terms. You must give appropriate credit, link to the license, indicate changes when applicable, and distribute adaptations under the same license or a compatible one.

Read the full license: https://creativecommons.org/licenses/by-sa/4.0/

## Author

Made by **evilsigmud**.

This project is a work in progress. Contributions, suggestions, and bug reports are welcome.

