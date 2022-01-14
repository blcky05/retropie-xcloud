# retropie-xcloud
Use Xbox Game Pass Cloud Gaming (xcloud) directly from within Retropie.

# Installation
All installation and configuration steps will happen in a command prompt.

## Install google chrome browser
Google chrome works very flawlessly with xcloud. You might also set-up another browser, hower you need to adapt the launch script.
* Downlaod the debian package
```
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
```
* Install the debian package
```
sudo dpkg -i google-chrome-stable_current_amd64.deb
```

## Add a new system to emulationstation
Copy the `es_systems.cfg` file to your retropie configs directory, s.t. an update will not overwrite your configuration.
```
sudo cp /etc/emulationstation/es_systems.cfg /opt/retropie/configs/all/emulationstation/es_systems.cfg
```
Replace `<your_username>` and append the following lines to `/opt/retropie/configs/all/emulationstation/es_systems.cfg` between the existing systems:
```
  <system>
    <name>xbox-gamepass</name>
    <fullname>Xbox Game Pass</fullname>
    <path>/home/<your_username>/RetroPie/roms/xcloud</path>
    <extension>.sh</extension>
    <command>/opt/retropie/supplementary/runcommand/runcommand.sh 0 _SYS_ xbox-gamepass %ROM%</command>
    <theme>xbox-gamepass</theme>
  </system>
```

## Copy the launch script
Copy the launch script, which will start google chrome in fullscreen app mode, to your roms folder of RetroPie
```
cd <repo_path>
cp --parents RetroPie/roms/xcloud/xcloud.sh ~/
```

## Finalize
* Now reboot emulationstation (or your device) to see the new entry in your emulationstation menu.
* Start the xcloud entry to see whether chrome opens app in fullscreen app mode and opens xcloud.
* If you want to stay logged in, accept all cookies. Otherwise reject them. (You'll need a keyboard to log-in)
* Have fun

# Improve

## Theme
* In order to make your new system entry look good, you can add some graphics to your current theme. These instructions are for the default carbon theme.
* Optional: Copy your current theme directory to your retropie configs directory, s.t. an update will not overwrite your configuration.
```
sudo cp -r /etc/emulationstation/themes/carbon-2021 /opt/retropie/configs/all/emulationstation/themes/carbon-2021-mod
```
* Get a vector graphic (.svg) for the systems image and for the controller image
** Recommendation for system: [Wikimedia](https://upload.wikimedia.org/wikipedia/commons/3/31/Xbox_Game_Pass_new_logo_-_colored_version.svg)
** Recommendation for controller: [Duimon's front-end assets](https://github.com/Duimon/Front-End-Assets/blob/main/EmulationStation/Carbon/xbox360/art/controller.svg)
* Copy the system svg to the `art/systems/` directory inside your copied theme directory
* Copy the controller svg to the `art/controllers/` directory inside your copied theme directory
* Rename both svgs to `xbox-gamepass.svg`
* Reboot your emulationstation or your system

## Controller hotkey
* In order to close the chrome browser rendering your xcloud games, you'll need a keyboard and a mouse (press ESC and click the X of the window header).
* You can use my [Retropie PCSX2 Wrapper](https://github.com/blcky05/retropie-pcsx2-wrapper), which will allow you to use your gamepad to close xcloud
* Set-up `Retropie PCSX2 Wrapper` and configure your controller as described in the other repo
* Modify the file `gamepad_wrapper.json` to add the xcloud system
** TODO