# ClickyXWin: Your Intelligent Windows Companion

ClickyXWin is a cutting-edge AI assistant designed specifically for the Windows operating system. It seamlessly integrates into your workflow by residing near your cursor, intelligently observing your screen, and executing tasks in the background to enhance your productivity and streamline your digital experience.

## Features

### The "Buddy" UI: Intuitive Cursor Tracking

ClickyXWin's user interface, affectionately known as the "Buddy," is engineered to be both **alive** and **non-intrusive**. It follows your cursor with a subtle, organic "spring" animation, ensuring it's always within your peripheral vision without distracting from your primary tasks.

*   **Technology**: Built using **WPF** (Windows Presentation Foundation) with `AllowsTransparency="True"` and `WindowStyle="None"` for a seamless, borderless appearance [3].
*   **Behavior**: Utilizes a low-level mouse hook (`SetWindowsHookEx`) for real-time cursor coordinate tracking, providing a fluid and responsive following experience [3].
*   **Visuals**: Features a sleek black-to-white color palette accented with light blue, expanding into a text input field or voice visualizer upon activation.

### Contextual Perception: The "Eyes" of ClickyXWin

To truly understand your context, ClickyXWin is equipped with advanced perception capabilities, allowing it to "see what the user sees" through high-frequency screen analysis.

*   **Screen Capture**: Leverages the **Windows Graphics Capture API** (available since Windows 10, version 1803) for low-latency, high-frame-rate capture of active windows or the entire desktop [1].
*   **OCR & Layout Analysis**: Integrates **Windows.Media.Ocr** for local text extraction and can send compressed frames to a Vision LLM (e.g., GPT-4o) for deeper semantic understanding of screen content.
*   **Active Window Tracking**: Continuously monitors the active application using `GetForegroundWindow` and `GetWindowText` to maintain metadata about your current operational context (e.g., "User is in Figma," "User is in VS Code").

### The "Clicky Agent": Intelligent Background Execution

ClickyXWin's core intelligence, the "Clicky Agent," operates in the background, performing tasks without interrupting your primary workflow. It employs a robust "Plan-Execute-Verify" loop to ensure efficient and accurate task completion.

*   **Task Orchestration**: Manages complex tasks through a structured planning and execution cycle.
*   **System Integration**:
    *   **File Management**: Utilizes `.NET System.IO` and **PowerShell** for comprehensive desktop organization, file manipulation, and content summarization.
    *   **Web Research**: Employs a headless browser (e.g., Playwright or Selenium) to conduct background web searches and extract relevant data.
    *   **Application Automation**: Interacts with third-party applications using the **Windows UI Automation (UIA)** framework, enabling actions like manipulating buttons and menus (e.g., "Turn this Figma into a webpage") [2].

## System Architecture Overview

ClickyXWin is built upon a layered architecture designed for performance and modularity:

| Layer | Component | Responsibility |
| :--- | :--- | :--- |
| **UI Layer** | WPF / WinUI 3 | Renders the "Buddy" (cursor-following widget) and handles user interaction. |
| **Perception Layer** | Windows Graphics Capture / OCR | Captures screen content and extracts text/context from the active window. |
| **Intelligence Layer** | LLM (GPT-4o / Claude 3.5) | Processes visual/textual context and generates responses or agentic plans. |
| **Action Layer** | UI Automation / PowerShell | Executes system-level tasks (file management, app control, web research). |

## Implementation Roadmap for LLMs

For developers and LLM integrators, the implementation of ClickyXWin follows a phased approach:

1.  **Phase 1: The Overlay**: Develop a transparent, top-most WPF window that accurately tracks and follows the mouse cursor using `User32.dll` hooks.
2.  **Phase 2: Screen Analysis**: Implement a module capable of capturing screenshots of the area around the cursor or the active window, and efficiently transmitting this visual data to a Vision API for analysis.
3.  **Phase 3: Voice/Text Interface**: Integrate advanced speech-to-text capabilities, such as **Azure Speech-to-Text** or **OpenAI Whisper**, to enable natural language interaction and "out loud" questioning.
4.  **Phase 4: Agentic Actions**: Construct a comprehensive library of **PowerShell** scripts and **Windows UI Automation (UIA)** patterns, allowing the LLM to programmatically interact with and manipulate the Windows environment.

## Key Technical Challenges

Developing an AI assistant like ClickyXWin presents several significant technical challenges:

*   **Performance**: Optimizing screen capture and LLM calls is crucial to prevent CPU spikes. This will involve techniques such as frame-differencing to process only changes on the screen, minimizing resource consumption.
*   **Privacy**: Implementing a robust "Privacy Mode" is essential. This mode will automatically halt screen capture when sensitive applications (e.g., password managers) are in focus, safeguarding user data.
*   **Z-Order Management**: Ensuring the "Buddy" UI consistently remains above all other windows without stealing focus from user input (e.g., typing) requires careful management of window Z-order.

## References

[1] [Windows Graphics Capture API](https://learn.microsoft.com/en-us/windows/uwp/audio-video-camera/screen-capture) - Official documentation for high-performance screen capture.
[2] [Windows UI Automation Framework](https://learn.microsoft.com/en-us/dotnet/framework/ui-automation/ui-automation-overview) - Guide for programmatically interacting with Windows applications.
[3] [WPF Transparent Windows](https://learn.microsoft.com/en-us/dotnet/desktop/wpf/windows/?view=netdesktop-8.0) - Technical details on creating non-rectangular, transparent overlays.
