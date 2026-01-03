


This GitHub repository (**windows-ai-agent-toolset-v1**) is a fresh proof-of-concept project demonstrating a lightweight, vision-based AI agent for automating Windows 11 desktop tasks. Overall, this is a neat, minimal take on "computer use" agents (like recent features from Anthropic/OpenAI), but **fully local and dependency-free**.

Solid foundation - excited to see if it evolves into more general tasks or broader toolsets!
If you have specific questions (e.g., feedback, improvements, or help testing), let me know.

### Strengths
- Extremely lightweight and portable (no pip installs needed).
- Precise coordinate handling for cross-resolution potential.
- Fully local/no cloud—great for privacy/experimentation.
- Impressive that a 2B-parameter model handles visual reasoning and tool use reliably enough for this demo.

### Limitations
- Tested only on 1080p resolution with specific DPI—no guarantees elsewhere.
- Task is hardcoded and simple (targeted at Notepad++).
- Small model can misinterpret visuals occasionally.
- Early-stage/experimental (only a single main script + logs/screenshots).

### Core Idea
The script uses the small **Qwen3-VL-2B-Instruct** vision-language model (run locally via LM Studio's OpenAI-compatible server) to "see" the screen via screenshots, reason step-by-step, and execute actions through tool calls. It requires **no external Python packages**—everything relies on built-in modules and direct Windows API calls via `ctypes` for screen capture, mouse control, clicking, typing, and scrolling.

### Key Features
- **Normalized coordinates**: All mouse movements use a 0–1000 scale (independent of resolution, mapped precisely to pixel positions).
- **Screenshot processing**: Captures full desktop via Windows GDI APIs, resizes with high-quality Lanczos filtering (default to 1344x756 for model input), encodes to base64, and embeds in prompts.
- **Tools available to the model**:
  - `take_screenshot`
  - `move_mouse(x, y)` (normalized)
  - `click_mouse`
  - `type_text(text)`
  - `scroll_down`
- **Minimal dependencies**: Pure Python + LM Studio running the model locally.
- **Low latency**: The 2B model processes quickly (~60 tokens/sec in logs).

### Demo Task
The hardcoded example prompt instructs the agent to:
1. Take a screenshot.
2. Move mouse to the center of a Notepad++ window.
3. Click.
4. Type "hello".
5. Take another screenshot.
6. Verify if "hello" is visible, and if so, scroll down once.

Repository screenshots show this working:
- Before: Notepad++ open in dark theme with an empty new file (multiple untitled tabs visible), plus overlapping windows like Command Prompt (running the script) and LM Studio logs.
- After: The word "hello" successfully typed into the editor.
- Annotated version: User-added red lines and an arrow highlighting the typed text area (possibly for emphasis or debugging).

### Setup & Running
1. Start LM Studio with the Qwen3-VL-2B-Instruct model in server mode (default localhost:1234).
2. Run `code.py`.
3. The script handles the loop: send prompt + current screenshot → model responds with reasoning + tool calls → execute tools → repeat up to max steps.

It logs progress, optionally dumps screenshots, and reports cursor positions (pixel + normalized).

No license file is included, so usage defaults to standard GitHub terms (view/share cautiously).

    ### (my original description)
    code and logs with screenshots from the real run
    
    This is a base for further improvements, the concept is working on the super small model, it may sometimes use center of a screen and not the notepad++ in the current hardcoded prompted schema but that is ok, it shows that THIS is a "good start" - #notetoself: whenever I will be stuck, use this as a reference of workflow that is working.
    
    Anyone who read this - just run the code (launch LM Studio earlier in the "server" mode, its meant to run on the same machine, localhost) and you will see a real ai making step by step actions on your real laptop/PC. There is no advanced "reasoning" implemented here, its more like proper setup of how to:
    -   take a screenshot using Windows 11 API (no pip install)
    -   use OpenAIApi to communicate between LM Studio and Script (Agent)
    -   everything is using "Normalized 0..1000" coordinates (which is crucial for simplicity and precision of moves,clicks regardless of screen size)
    -   a good description of the tools, system and user task
    
    **VALIDATION:**
    Tested on 1080p with scale 100% Windows 11 (it uses resizing for speedup anyway but if it works on different monitor sizes and scales of them - I am not sure yet,
    
    I am going to improve this version on my specific monitor setup for now to not waste a time for edge use cases - it may work with different resolutions due to Context Aware V2 DPI but I wont test it as for now, its not the main goal at this moment to check this)
    
    **WHY ITS IMPORTANT REPOSITORY:**
    I have finally achieved to connect all the basic mechanism and calculations to achieve precision (not even the model precision is important here but the screenshots/coordinates/tools usage precision - TO MAKE A CLICK ON A SPECIFIC PLACE ON THE SCREEN - this was the tough part, that was the part on which I have spent the most of the time.
    
    **NEXT STEP:**
    Debug the prompts and get the most precision from the model itself. Add logging to be extra sure about the coordinates calculations - I see that its working now but I dont have a general "mathematical" proof yet and thats ok, as for this version of the repository, everything is fine.
    
    **IT WORKS!**
