# sd72-project-elysium
The Elysium Fields are a paradise for the heroic and virtuous after death.  In this case, the death of old student laptops.

# Creating the image
 - CUBIC to generate
 - balenaEtcher to create USB installer

# Desktop Environment
- Lubuntu (Ubuntu with LXQt).  Fast but ugly
- Linux Mint with Cinnamon - Ideal if it's fast enough
- Linux Mint with XFCE - Try if Cinnamon is too slow

# Requirements / TODO
  - [x] No listed users at login screen
  - [x] Guest session option only at login screen:
      - [x] Enable guest session
      - [x] Remove admin login option from greeter
      - [x] Update Temporary Guest Session popup message
  - [x]  No popups or other stuff on first login by Guest (Can do this by getting a copy of the usr/skel or by creating a defaul user skel, after dismissing all the things and setting up as needed)
      - [x] Linux Mint Welcome
  - [ ] enable firewall? (ufw)  
  - [x] Chrome installed
  - [x] Chrome auto opens to office365 or teams page for login to school account
  - [x] Ensure VLC and all Codecs are installed `apt install vlc
  - [ ] Turn off anything that autostarts and run uneccessarily
  - [x] Remove LibreOffice
  - [ ] Ensure everything deleted (guest home account) when use logs off
  - [ ] Background image? `sudo cp /path/to/your-image.jpg /usr/share/backgrounds/linuxmint/default_background.jpg`
  - [ ] Login screen image? - replace all the throbber and animation images in `cd /usr/share/plymouth/themes/mint-logo/`
  - [ ] Screensaver?
  - [ ] Auto connect to wifi, how? Preseed?
  - [ ]  ? 

# Decisions

 - LVM? Off (either works.  https://serverfault.com/questions/209461/lvm-performance-overhead/1130851#1130851)
 - https://easylinuxtipsproject.blogspot.com/p/first-mint-cinnamon.html
 - https://easylinuxtipsproject.blogspot.com/p/speed-mint.html#ID1
 - https://easylinuxtipsproject.blogspot.com/p/ssd.html#ID2
 - https://wiki.ubuntu.com/LightDM#Configuration
 - https://help.ubuntu.com/community/CustomizeGuestSession

# Configuration

## Unattended Upgrade / Automatic Updates:

https://help.ubuntu.com/community/AutomaticSecurityUpdates#Using_the_.22unattended-upgrades.22_package

Also remove Mint-Update: `sudo apt remove --purge -y mintupdate`

## Preseed
apt install debconf-utils

so can dump the selected settings with:  
https://wiki.debian.org/DebianInstaller/Preseed


## Greeter and Guest Mode

### Greeter
Greeter docs: https://wiki.ubuntu.com/LightDM#Configuration
nano /usr/share/lightdm/lightdm.conf.d/99-sd72.conf
```
[Seat:*]
allow-guest=true  
greeter-hide-users=true
autologin-guest=true
#greeter-show-manual-login=true  # testing only, turn off for production  
```

### Popup message
Disable default: https://help.ubuntu.com/community/CustomizeGuestSession#Disable_startup_dialog

nano /etc/guest-session/prefs.sh
```
touch $HOME/.skip-guest-warning-dialog
```

Replace with new popup message (that won't be overwritten if LightDM updates per https://askubuntu.com/a/533257)
nano /etc/guest-session/auto.sh
```
TITLE='Temporary Guest Session'
TEXT="All data created during this guest session will be deleted
when you log out and settings will be reset to defaults.

Please save files to your Microsoft OneDrive if you would
like to access them again later."
{ sleep 4; zenity --warning --no-wrap --title="$TITLE" --text="$TEXT"; } &
```

### Background Default


### Loading Icons


### Guest Account



Configuring the default guest home drive skeleton (see https://help.ubuntu.com/community/CustomizeGuestSession)
1. Open Google Chrome, set the Keyring password to blank (to prevent it from popping up everytie)
2. Pin Chrome to the bottom bar
3. Run Chrome and Firefox and get rid of all the first-time popups/windows/questions
4. Set the start pages (startup tabs for Chrome and Firefox Home Shortcuts):
   - https://login.microsoftonline.com
   - https://teams.microsoft.com/v2/
   - https://www.sd72.bc.ca/ 
5. Run "Startup Applications" app:
   - Add Google Chrome
   - Turn off: SSH Key Agent, Support for NVIDIA Prime, System Reports
7. Edit the Firefox newtab/home page (cog top right of page) and turn off recommended stories, Recent activity, and Weather.  Remove default shortcut tiles below the google search bar and add the three listed above
8. Delete history from Chrome and Firefox (so the default login guest has empty history)
9. Remove the terminal from the bottom bar (it's pinned by default)

Now need to install this as the default guest home (home drive skeleton that is copied to a the new ephemeral guest user when logging in):
copy the home drive to: `/etc/guest-session/skel`

## Chrome
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb  
dpkg -i google-chrome*.deb  

## Keyring (Chrome problem)
https://forums.linuxmint.com/viewtopic.php?t=431888  
sudo apt-get install libpam-gnome-keyring  
sudo nano /etc/pam.d/lightdm  
auth optional pam_gnome_keyring.so  # not commented out  
session optional pam_gnome_keyring.so auto_start  # not commented out  

## Upgrade everything and clean caches
```
sudo apt full-upgrade
du -sh /var/cache/apt/archives/ # check cache size
apt autoremove 
apt full 
du -sh /var/cache/apt/archives/ # check cache size
```

## CUBIC package selection
Remove these packages (untick) during Cubic iso creation

 - manpages
 - timeshift
 - transmission
 - thunderbird
 - totem
 - rythmbox
 - hypnotix
 - libreoffice-*
 - simple-scan
 - nvidia-prime-applet
 - yelp-*
 - pidgin
 - hexchat

