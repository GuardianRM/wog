Heroes 3.5: In the Wake of Gods 3.59 alpha.
===

About
---

This is Alpha, so anything may change in future.  
Team interaction would happen via Skype: sergroj_(my GitHub nickname).
WoG 3.59 is going to be a platform hosting different mods, somewhat like Era II in that sense, but different.  
Alpha version executable is called WogT1.exe for historic reasons. Executable of final version will be called h3wog.exe as usual.

===

Installing a release
---

Extract contents to WoG home folder. Using a folder with clean WoG 3.58 install is preferable. Make sure Data folder doesn't contain these files:  
ARTEVENT.TXT  
ARTRAITS.TXT  
CRANIM.txt  
CRTRAITS.TXT  
SpTraits.txt  
ZCRTRAIT.TXT  
ZELP.TXT  

Note: If you're building WoG from sources, the only thing you'll need from a release is Data\p\ folder, but you must get rid of text files mentioned above.

===

Testing
---

'info' folder contains descriptions of new 3.59 stuff (and t1.map file for my own debugging convenience). Mods folder contains all scripts, Data\s\ isn't used anymore.

Saved games from 3.58 are incompatible and from one version of 3.59a to another saves compatibility may break as well.

If WoG happens to hang, don't kill the process. Instead, use this program: https://dl.dropboxusercontent.com/u/44735333/tmp/WindowMan.rar  
Run it, then switch to WoG window and switch back to the program. It should pick up the window name of WoG. When you see it's correct, press the "Crash" button. This will make WoG create WOGCRASHLOG.TXT and WOGERMLOG.TXT logs. The program itself will create CrashEIP.txt file in its own folder. Send me all 3 files.

In addition to sending WOGCRASHLOG.TXT, WOGERMLOG.TXT and/or WOGLUALOG.TXT don't forget to describe what exactly you did that lead to the issue and send the save game and map if they're relevant.

Also, setting No32Bit=0 in [Common] of WoG.ini will let you run WoG windowed in 32-bit screen mode. However, 10-60 minutes into the game it will hang. That's ok, 32 bit mode code is temporary. Baratorch's HD Mod does it much better, so it should be the base of future proper 32 bit mode support.

===

Building
---

- The project is for Visual Studio 2005. I haven't tried Express edition, but here are some links:  
http://go.microsoft.com/fwlink/?linkid=57034 (Express Edition)  
http://cplus.about.com/od/learnc/ss/vcpppins.htm (About installation)  
http://www.microsoft.com/en-us/download/details.aspx?id=804 (Service Pack 1, I don't know if the first link includes it or not)

- Add %HOMMWOGDIR% to environment variables, set it to the path where WoG is installed. Restart VS if it's running.

- In WoG.ini add these lines:

```ini
[Common]
DeveloperPath=(path to the repository)
AllowMultipleCopies=1
```

Done! Now you can build and run the project. Use "Dll" configugation for debugging. "Release" configuratin is used for deployment. The t1.map file found in Build folder can help you debug it.

===

About Code
---

To find code of a receiver (let's say, 'UX'), search in erm.cpp for its name like this: 'UX'.

Internal numbers of triggers are listed after ERM_Triggers table in erm.cpp. To find code that calls a trigger you need to search for its number (use "Find in Files" in VS).

All new code hooks are in global_hooks.h and global.cpp files as well as Lua files. Old hooks are in _B1.cpp. Don't do hooks the old way!

Note the WogNew project. The reason it's there is because t1b project must be built with optimization turned off, due to functions intermixing C code with Asm. This is also one of the reasons the solution is for VS 2005.

===

About Git
---

You may want to hide a local folder from Git. E.g. I have a mod with my test scripts. To do so, create .gitignore file in it containing just this:

```
/*
```
