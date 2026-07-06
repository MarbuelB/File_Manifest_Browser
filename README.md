# Storage Manifest Viewer

An interactive, zero-install, single-file client-side web application designed to locally visualize, browse, and audit deep-storage file archives. Operating entirely offline in your modern web browser, this tool processes snapshot logs from both Linux and Windows environments, parsing raw text lines into a navigable, scalable virtual directory tree.

## Key Features

* **Zero Local Software:** Runs fully localized within any modern browser window (Chrome, Edge, Firefox). Requires no local web servers, node environments, or installation scripts.
* **Native Browser Auto-Generation:** Leverages the modern File System Access API to scan local folders and auto-generate manifest logs directly inside the browser, no terminal required!
* **Smart Root Navigation:** Automatically calculates the deepest common folder across all loaded files and jumps you straight there, skipping empty, linear parent directories.
* **Native Browser History Integration:** Automatically syncs folder traversal with the browser's History API, allowing seamless use of the native Back and Forward buttons for navigation.
* **Dual-Format Auto-Detection Engine:** Line-by-line smart format interpretation that seamlessly reads standard Linux file system trees and native Windows command logs side-by-side.
* **Native OS Path Handling:** Parses, renders, and manages file paths using their true operating system separator (`\` for Windows, `/` for Linux) natively, ensuring perfect accuracy for copying paths and system integration.
* **Interactive Tree Browser:** Dynamically aggregates independent snapshots under a single unified virtual Root node, automatically merging overlapping directory branches while preserving distinct target file objects.
* **Advanced Boolean Query Parser:** Full client-side Boolean implementation backing case-sensitive operators (`AND`, `OR`) alongside parentheses `()` for processing highly customized logic stacks.
* **Multi-Scope Targeted Searching:** Divided control inputs allowing isolated filter rules applied to individual File/Folder Names, Absolute File System Paths, or combined criteria concurrently.
* **Granular Numerical Sizing Bounds:** Configurable "From" and "To" size-range parameters supporting automated mathematical translations across KB, MB, and GB bounds.
* **Wildcard Mask Matching:** Complete support for global execution patterns like `*` for multi-character sequences and `?` for targeted single-character tracking.
* **Cumulative Memory Context:** Re-engineered ingestion pipelines that append newly selected assets to the current viewport dynamically instead of overwriting existing catalog records.
* **Automated Suffix Deduplication:** Intelligent indexing that identifies overlapping filename imports and assigns custom tags (`#2`, `#3`, etc.) to isolate individual source manifest filters.
* **Draggable Header Resizers:** Native grid boundary tracking allowing you to click-and-drag table borders to configure column widths dynamically.
* **Click-to-Open Redirection:** Leverages native browser handling to open target paths on your system using the `file://` scheme straight from the table.
* **Isolated Profiling Unloader:** Integrated utility triggers (🗑️) to wipe targeted manifest allocations cleanly from active browser memory stacks without reloading the interface.

---

## Getting Started

### Installation
Because the application is fully standalone, setup requires only saving the `file_manifest_browser.html` file locally. Double-click the file to open it natively in your browser.

---

## Manifest Generation Commands

### 1. Automatic Client-Side Generation (Recommended)
You can generate manifest files directly from the browser without using terminal commands! 
1. Click the **🪄 Auto-Generate** button in the top left.
2. Select any folder on your local computer.
3. If prompted, paste the absolute path of your folder to ensure all file links are fully clickable.
The browser will securely scan the folder, save a `.manifest` file for your records, and instantly load the results into the viewer.

---

### 2. Manual CLI Generation
To view file layers of remote servers or environments where the browser cannot access the file system directly, create snapshot files using these native operating system terminal commands:

#### In Linux Environments
Run the standard find command utilizing the long-listing flag to output the precise 11-column string format:

    find /path/to/target/folder -ls > linux.manifest

#### In Windows Environments
Run this custom pipeline string from a native administrative PowerShell console window to construct an equivalent pipe-delimited output string:

    gci "C:\path\to\target\folder" -r | % { "$($_.Mode)|$($_.Length)|$($_.LastWriteTime)|$($_.FullName)" } > windows.manifest

---

## Advanced Search Queries

The application features a dedicated custom Shunting-Yard tokenization algorithm to process logical syntax layers.

### Operator Case Sensitivity
* To prevent literal terms within filename strings (e.g., matching the word "and" inside "Andrea") from splitting the token analyzer, logical commands **MUST** be entered in absolute capital letters (`AND`, `OR`, `NOT`).
* Lowercase string variations like `and` or `not` are interpreted as plain, literal search terms.

### Explicit Precedence Grouping
The search parser processes inputs in standard mathematical priority order (`NOT` is resolved first, followed by `AND` queries, and finally `OR` branches). Use parentheses `()` to enforce custom logical conditions.

### Wildcard Logic (`*` and `?`)
* If an input contains no wildcards, it performs a default "contains" string lookup.
* If a wildcard token is found, the engine switches to an exact start-to-finish mask evaluation.
    * Use `*` to indicate any number of characters.
    * Use `?` to target exactly one character.

### Filtering Query Examples

* Name Search Example:
    e.g. (.pdf OR .ppt) AND present*

* Path Search Example:
    e.g. (scicore OR group) AND (data OR raw)

---

## Technical Architecture Notes

* **Data Lifecycle:** File ingestion is processed purely within local tab memory context via the asynchronous HTML5 `FileReader` API. No server-side transfers, cookie logs, or analytics frames are used. 
* **Virtual Tree Traversal:** Directory scopes are tracked inside an active folder string state variable (`currentPath`). When this state is empty (`''`), a root loop dynamically interprets the first level of divergent paths (e.g., `/scicore/...` vs `C:/...`), rendering unique top-level containers cleanly.
* **Render Throttle Thresholds:** The user interface applies a rendering protective roof set to a maximum limit of 2,000 active table rows per filter configuration. This safeguards standard browser DOM elements against memory exhaustion when traversing multi-million row file sheets.
