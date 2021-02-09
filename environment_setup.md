# Environment setup

This document describes how to set up your computer and install all the tools 
required to develop Open Source projects at Fragile Tech.

We recommend installing any GNU/Linux OS, but this guide will target a fresh installation of 
[Ubuntu 20.04](https://ubuntu.com/download/desktop)

## Communication tools

### [Zoom](https://zoom.us/)
Videoconference tool. We will use Zoom for our weekly meeting every Wednesday at 18:30, and to catch
up if needed.

#### Installation
- Download the .deb package from [here](https://zoom.us/client/latest/zoom_amd64.deb)
- Open the download file and click install on the graphic interface.

### [Calendly](https://calendly.com/)
Configure a Calendly account and create a calendar with the hours that you plan to spend working on
the Fragile Guide.

You can schedule a meeting with [Guillem](https://calendly.com/guillemdb/fragile-guide) if you need any kind of support.

## Development tools

### [PyCharm CE](https://www.jetbrains.com/pycharm/download/#section=linux)
IDE for developing Python projects.

#### Installation
`sudo snap install pycharm-community --classic`

#### Setup

**Custom fonts**
  1. Download the [Hack](https://github.com/source-foundry/Hack/releases/download/v3.003/Hack-v3.003-ttf.zip) fonts (optional)
  2. Install the fonts
  3. Open settings (`file`->`settings` or `Ctrl+Alt+s`) go to `Editor`->`Font` and choose your desired font and font size.
    
**Change theme**
  1. Open settings and go to `Editor`->`Appearance & behavior`->`Appearance`
  2. Select the theme you like the most. (I recommend `Darcula`.)
  
**Visual guides**
  1. Open settings and go to `Editor`->`Code Style`
  2. Set `Hard wrap` to `99` and `Visual guide` to `80`.
  
**Configure documentation**
  1. Open settings and go to `Editor`->`Tools`->`Python integrated tools`.
  2. Set `Testing`->`Default runner` to `pytest`.
  3.  Set `Docstrings`->`Dosctring format` to `Google` and check both tick boxes.

**Resize font using the mouse wheel**
  1. Open settings and go to `Editor`->`General`
  2. In the section `Mouse control` tick the box `Change font size with ctrl+Mouse Wheel`.

### [GitKraken](https://www.gitkraken.com/git-client)

Git GUI client.

#### Installation
`sudo snap install gitkraken --classic`
