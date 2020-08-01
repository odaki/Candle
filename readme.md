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

Build requirements:
------------------
Qt 5.15.0 with Xcode commandline compiler (Apple clang version 11.0.3)

Downloads:
----------
Experimental versions:

* [Version 1.2.8b release](https://github.com/odaki/Candle/releases)

"Candle" main window:
![screenshot](/screenshots/screenshot_macos.png)
