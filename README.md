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
  - [ ] No listed users at login screen
  - [ ] Guest session option only at login screen:
      - [ ] Enable guest session
      - [ ] Remove admin login option from greeter
      - [ ] Update Temporary Guest Session popup message
  - [ ] No popups or other stuff on first login by Guest (Can do this by getting a copy of the usr/skel or by creating a defaul user skel, after dismissing all the things and setting up as needed)
      - [ ] Linux Mint Welcome
  - [ ] enable firewall? (ufw)  
  - [ ] Chrome installed
  - [ ] Chrome auto opens to office365 or teams page for login to school account
  - [ ] Ensure VLC and all Codecs are installed
  - [ ] Turn off anything that autostarts and run uneccessarily
  - [ ] Remove LibreOffice, instead have shortcuts linked to web versions of Word/Excel/other?
  - [ ] Ensure everything deleted (guest home account) when use logs off
  - [ ] Background image?
  - [ ] Login screen image?
  - [ ] Screensaver?
  - [ ] Auto connect to wifi, how? Preseed?
  - [ ]  ? 

# Decisions

 - LVM? Off (either works.  https://serverfault.com/questions/209461/lvm-performance-overhead/1130851#1130851)
 - https://easylinuxtipsproject.blogspot.com/p/first-mint-cinnamon.html
 - https://easylinuxtipsproject.blogspot.com/p/speed-mint.html#ID1
 - https://easylinuxtipsproject.blogspot.com/p/ssd.html#ID2
 - https://wiki.ubuntu.com/LightDM#Configuration

# Configuration

## Greeter and Guest Mode

