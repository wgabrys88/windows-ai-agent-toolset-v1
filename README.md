code and logs with screenshots from the real run
This is a base for further improvements, the concept is working on the super small model, it may sometimes use center of a screen and not the notepad++ in the current hardcoded prompted schema but that is ok, it shows that THIS is a "good start" - #notetoself: whenever I will be stuck, use this as a reference of workflow that is working.

Anyone who read this - just run the code (launch LM Studio earlier in the "server" mode, its meant to run on the same machine, localhost) and you will see a real ai making step by step actions on your real laptop/PC. There is no advanced "reasoning" implemented here, its more like proper setup of how to:
- take a screenshot using Windows 11 API (no pip install)
- use OpenAIApi to communicate between LM Studio and Script (Agent)
- everything is uing "Normalized 0..1000" coordinates (which is crucial for simplicity and precision of moves,clicks regardless of screen size)
- a good description of the tools, system and user task

VALIDATION:
Tested on 1080p with scale 100% Windows 11 (it uses resizing for speedup anyway but if it works on different monitor sizes and scales of them - I am not sure yet,
I am going to improve this version on my specific monitor setup for now to not waste a time for edge use cases - it may work with different resolutions due to Context Aware V2 DPI but I wont test it as for now, its not the main goal at this moment to heck this)

WHY ITS IMPORTANT REPOSITORY:
I have finally achieved to connect all the basic mechanism and calculations to achieve precision (not even the model precision is important here but the screenshots/coordinates/tools usage precision - TO MAKE A CLICK ON A SPECIFIC PLACE ON THE SCREEN - this was the tough part, that was the part on which I have spnt the most of the time.

NEXT STEP:
Debug the prompts and get the most precision from the model itself. Add logging to be extra sure about the coordinations calculations - I see that its working now but I dont have a general "mathematical" proof yet and thats ok, as for this version of the repositry, everything is fine. IT WORKS!
