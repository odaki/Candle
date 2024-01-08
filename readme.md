Candle
-----------
GRBL controller application with G-Code visualizer written in Qt.

Supported functions:
* Controlling GRBL-based cnc-machine via console commands, buttons on form, numpad.
* Monitoring cnc-machine state.
* Loading, editing, saving and sending of G-code files to cnc-machine.
* Visualizing G-code files.

Changed from base repository:
------------------
* Based on [Experimental release](https://github.com/Denvi/Candle/tree/Experimental)
* Adoption of a new version of Qt
* Change CMakeLists.txt to generate DMG package (run "make appdmg")
* Disable plugins
* Support Apple Silicon
* Open G-Code from Finder

Build requirements:
------------------
Qt 5.15.x with Xcode commandline compiler (Apple clang version 15.0.0)

Downloads:
----------
Experimental versions:

* [Version 1.2.9.1b release](https://github.com/odaki/Candle/releases)

Before creating new issue:
------
Candle works with CNC controlled by GRBL firmware, many problems can be solved by using proper version of GRBL, using proper configuration.

Please read GRBL wiki: 
- GRBL v0.9-: https://github.com/grbl/grbl/wiki
- GRBL v1.1: https://github.com/gnea/grbl/wiki

"Candle" main window:
![screenshot](/screenshots/screenshot_macos.png)
