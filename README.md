# vscode-circuitpython README

This extension aspires to bring your entire CircuitPython workflow into a single
place in VSCode.  

Inspired by [Scott Hanselman's blog
post](https://www.hanselman.com/blog/UsingVisualStudioCodeToProgramCircuitPythonWithAnAdaFruitNeoTrellisM4.aspx)
and the [VSCode Arduino extension](https://github.com/Microsoft/vscode-arduino).

## Getting Started

The extension will currently activate when any of the following occur:

* workspace contains
  * `/code.py`
  * `/code.txt`
  * `/main.py`
  * `/main.txt`
  * `/boot_out.txt`
* command run
  * `circuitpython.openSerialMonitor`
  * `circuitpython.selectSerialPort`
  * `circuitpython.closeSerialMonitor`

Upon activation, the extension will check for the latest
[Adafruit_CircuitPython_Bundle](https://github.com/adafruit/Adafruit_CircuitPython_Bundle)
and download it if needed. It'll then load that library metadata into the
workspace's state. You can also trigger this manually with `CircuitPython: Check
for latest bundle`.

After that you should be ready to use the following features.

## Features

### Library Management

v0.0.2 introduced a [Circup](https://github.com/adafruit/circup) inspired
library manager, with an emphasis on VSCode integration. It downloads new
bundles automatically.

You can use it with the following commands:

* `CircuitPython: Show Available Libraries`
  This is every library in the Adafruit Bundle. Alphabetical, but 
  installed libraries are grouped on top. Click an out of date library 
  to update, click an uninstalled library to install it.
* `CircuitPython: List Project Libraries`
  Lists what's in your project's lib. If anything is out of date, click 
  it to update.
* `CircuitPython: Reload Project Libraries` 
  In case it's reporting incorrectly. This can happen if you modify the 
  filesystem outside of vscode.
* `CircuitPython: Update All Libraries`
  Equivalent of `circup update --all`
* `CircuitPython: Check for latest bundle`
  Compares the bundle on disk to the latest github release, downloads the 
  release if it's newer.

### Serial Console

`Circuit Python: Open Serial Console` will prompt you for a serial port to
connect to, then it will display the serial output form the board attached to
that port. The port can be changed by clicking on it's path in the status bar.

Hit `Ctrl-C` and any key to enter the Circuit Python REPL, and `Ctrl-D` to
reload.

Note: There are linux permissions issues with the serial console, but if you're
on linux, you're probably used to that.

It will also change your workspace's default `board.pyi` file for autocomplete
to the one that matches the USB Vendor ID & Product ID.

If you want to manually choose a different board, a list is available with the
command `CircuitPython: Choose CircuitPython Board`, and also by clicking on the
board name in the status bar.

**NOTE FOR WINDOWS USERS**: I have seen trouble with the serial console,
displaying anything at all. If that happens, try launching VSCode as an
administrator and see if it works. I have even gotten it to work as a
non-administrator after this, so perhaps running it as an admin stole the serial
port from whatever was using it, and then whatever it was didn't grab it again.

### Auto Complete

Automatically adds stubs for your specific board, the circuitpython standard
library and all py source files in the adafruit bundle to your completion path.

### Demo

![Demo](images/circuitpy-demo.gif)

## Requirements

## Extension Settings

### Board Settings

Board specific settings can be stored in a project's `.vscode/settings.json`
file, which will default to this board. This is great for when opening up the
CIRCUITPY drive as a vscode workspace, and will be automatically set every time
you choose a board.

You can also use this for projects you're working from on disk, with the intent
of running on a specific board.

You can also set these at a user level, although that's not the primary intent.
If you do this, it will get overridden at the workspace level if you ever touch
the choose board dropdown or open a serial monitor. 

I'd probably have restricted the scope to workspace if that was an option.

`circuitpython.board.vid`: Vendor ID for the project's board
`circuitpython.board.pid`: Product ID for the project's board
`circuitpython.board.version`: Persisted for choosing the right mpy binaries

## Known Issues

## Release Notes

See the [Changelog](CHANGELOG.md)
