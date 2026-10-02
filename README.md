# LayerDrop-V2.2
A free Premiere Pro panel that adds adjustment layers and color mattes in one click. Select your clips, click a button, and Layer Drop places each layer on the first free track above them, trimmed to the right length.
Requirements
Adobe Premiere Pro 2022 or later (tested target: 2025)
Windows or macOS
Installation
1. Download

Click Code > Download ZIP on this page (or download the latest release), then unzip it.

You should end up with a folder that has CSXS, jsx and index.html directly inside it. The folder name doesn't matter, but these files must not be nested one level deeper.

2. Allow unsigned extensions (one time only)

Premiere only loads signed extensions by default, so you need to turn on debug mode once.

<H1>Windows</H1>

Press Win + R, type regedit and press Enter.
Go to HKEY_CURRENT_USER\Software\Adobe\.
Open the key CSXS.12. If it doesn't exist, right-click Adobe, choose New > Key, and name it CSXS.12.
Inside it, right-click an empty area, choose New > String Value, and name it PlayerDebugMode.
Double-click it and set the value to 1.
Repeat steps 3 to 5 for CSXS.11.

<H1>macOS</H1>

Open Terminal and run:

bash
defaults write com.adobe.CSXS.12 PlayerDebugMode 1
defaults write com.adobe.CSXS.11 PlayerDebugMode 1
3. Copy the folder

Move the unzipped folder into Premiere's extensions folder. Create the CEP and extensions folders if they don't exist.

OS	Path
Windows	%APPDATA%\Adobe\CEP\extensions\
macOS	~/Library/Application Support/Adobe/CEP/extensions/

On Windows you can paste the path into Win + R. On macOS, press Cmd + Shift + G in Finder and paste it.

4. Open the panel

Restart Premiere Pro, open a project and go to Window > Extensions > Layer Drop. Dock it next to your timeline.

First-time setup in each project

Premiere's scripting can't create adjustment layers or color mattes from nothing, so Layer Drop needs one of each to copy from.

Go to File > New > Adjustment Layer and click OK.
Go to File > New > Color Matte, pick a color and click OK.
Press Check again in the panel.

Layer Drop moves them into a bin called Layer Drop and reuses them from then on. You only do this once per project.

How to use
Action	Result
Click with clips selected	A layer over each selected clip, matching its length
Shift + click, one clip selected	A short layer at the start of that clip
Shift + click, two or more clips selected	A short layer centered on each cut between them, half before and half after
Ctrl + click (Cmd on Mac)	One layer spanning all selected clips
Alt + click (Opt on Mac), or nothing selected	A layer at the playhead

Short layers (cuts and playhead) use the Default length setting. With an odd number of frames, the extra frame goes after the cut.

<H1>Settings</H1>

Open Settings in the panel to change:

Default length: the length of cut and playhead layers, in frames.
Adjustment effect: an effect added to every new adjustment layer. Choose Other to type the exact name of any built-in Premiere effect.

Your settings are remembered between sessions.

Troubleshooting

Layer Drop isn't in Window > Extensions

Check that PlayerDebugMode is set to 1 (step 2), then restart Premiere fully.
Check that CSXS is directly inside the folder you copied, not inside another folder.

"No adjustment layer found yet" Do the first-time setup above for this project.

"Effect not found" or "couldn't attach effect" The layer is still placed, but the effect wasn't added. Check the effect name matches Premiere's Effects panel exactly, or add it by hand.

"No free track" Add a video track above your clips and try again.

<H1>Known limitations</H1>
Matte colors are shared. All placed mattes come from one source, so recoloring one recolors them all. For a second color, duplicate the matte in the bin, recolor the copy and drag it in manually.
Saved presets aren't supported. Only built-in effects can be auto-applied.
No built-in keyboard shortcuts. Panels can't register their own. Use a macro tool such as AutoHotkey (Windows) or Keyboard Maestro (macOS) to click the buttons.
Auto-effect relies on an undocumented Premiere API and may behave differently between versions.
Built on CEP. Adobe is moving extensions to UXP, so a future Premiere version may need a port.
Feedback

Found a bug or have an idea? Open an issue and include your Premiere version, your OS and the exact message shown in the panel's status line.
