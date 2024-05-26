# Look for updates at the end of the document
## Hello all


I know this solution comes very late, but I responded to a request on how to change the built-in Calendar icon in macOS Big Sur, macOS Monterey, macOS Ventura, macOS Sonoma

I wanted to in addition to my comment elsewhere help people with a standalone posting about the topic.

Ready? Okay, Let's go. Wait.. before we get too far along I'd like to write a disclaimer for my own good.

**I HOPE THAT YOU KNOW THAT I'M NOT ATTEMPTING TO DAMAGE YOUR MACOS BIG SUR, MACOS MONTEREY, VENTURA OR SONOMA SETUP
I HAVE TRIED THIS METHOD OF CHANGING OF ICONS AND THEME FILES MANY TIMES AND I CONSIDER MYSELF QUITE KNOWLEDGEABLE WHEN IT COMES TO THEMING MACOS AS I'VE MADE QUITE A FEW ALTERATIONS FOR VARIOUS ITERATIONS OF MACOS - DATING BACK TO AT LEAST MAC OS X LION. WITH OS X MAVERICKS I MADE A WHOLE SLEW OF FLAVOURS THEMES AND I'VE CONTINUED MAKING THEMES, CURSORS AND OTHER ITEMS FOR MACOS SINCE THEN**

with love, Allan Nyholm Nielsen
[https://www.deviantart.com/allannyholm/gallery/]()

Download the code here and also get a Calendar icon made by me.

# SOLUTION

**In the recovery Terminal window type - one at a time**
```
csrutil disable
```
&
```
csrutil authenticated-root disable
```

**REBOOT to the macOS Big Sur desktop**
```
shutdown -r now
```

# APPLE SILICON SOLUTION

### Shutdown your Apple silicon-based Mac

**Next hold down the power button for a few seconds. On a Mac mini you'll see the front power light dim a little. You should now let go of the power button**

**In the recovery Terminal window type - one at a time**
```
csrutil disable
```
Enter user password. Wait a little while.

Next enter
```
csrutil authenticated-root disable
```
Again, enter your user password. Wait a little while. Reboot.

_**My experience: You'll be required to enter your user password for both these operations when on an Apple Silicon Mac. And you also have to have macOS user already set up**_

## REQUIRED READING FOR THIS WHOLE THING TO WORK
I urge you to read up on the entry this ThemeEngine fork by Jeremy Legendre that explains how to change theme files on modern macOS’ like Big Sur and macOS Monterey. It's really the only option at this point.

Outgoing link to readme
[https://github.com/jslegendre/ThemeEngine#readme]()

Download latest compatible version for macOS Sonoma. Version 118 at this writing.


# TRICKS AND TRICKERY LOCATING AND CHANGING THE CALENDAR ICON ON THE SYSTEM

### **CALENDER DOCK TILE ICON PATH**
> /System/Library/PrivateFrameworks/CalendarUIKit.framework/Versions/A/Resources/App-empty.icns

You can only change this icon after opening up the system by means explained in the link above. Basically you change the icon in the newly made location that you’ve set up. 

Be aware that you’ll be required to both locate and change the icon in this path, not via the top level Mac drive structure, but from the newly made directory where you from now on will change **ALL YOUR SYSTEM FILES** for the purpose of changing the Calendar and system level theme files.

## **LESSON**
Remember to use the ```bless```  command after you’re done - again described great by Jeremy Legendre in his readme)

**Reboot your Mac while in the Terminal**
```
sudo shutdown -r now
```


# I WILL NOW USE MY OWN WORDS TO HELP YOU

1. Create a directory in your Home directory with a name that will make sense for your theming efforts.
In this example I call the directory 'livemount'
2. Open Terminal
3. Type in ```mount```
4. Find the top-most drive listed e.g _disk2s5s1_ this is something different for most users
5. Type ```sudo mount -o nobrowse -t apfs /dev/disk2s5 /Users/yourusernamehere/livemount/```  

> _notice the last entry of the disk name is missing in the disk name above: s1_

6. Navigate to ```/Users/yourusernamehere/livemount/```
7. Now you ought to see your system disk mounted in this folder
8. Navigate to ```/System/Library/PrivateFrameworks/CalendarUIKit.framework/Versions/A/Resources/```in that system disk within that folder you made called livemount
9. Change the App-Empty.icns file
10. Type ```sudo bless --mount /Users/yourusernamehere/livemount/ --bootefi --create-snapshot```
11. Wait a second or 2 for the blessing of your system disk to complete
12. Type ```sudo shutdown -r now```
13. Alternatively you can use the Finder - Restart... menu item.
14. Your Mac reboots
 

## **IF YOU FOLLOW ALL INSTRUCTIONS YOU WILL HAVE CHANGED THE ICON.**


# UPDATE 28th of October 2021
## The Calendar icon inside Launchpad and how to change that too.

- The exact same process as mentioned earlier
- This time instead you'll want to change the Calendar icon inside ```/System/Applications/Calendar/Contents/Resources/Assets.car```
- You will need ThemeEngine to change the icons in here as it can edit and save out the ```.car``` file you need.
- Best practice for changing system files is to **always make backups!**

  
# UPDATE 20th of March 2024
## The Calendar icon on ARM
- When you're using an Apple Silicon Mac you'll need to change the bless command a little. If all you're doing is changing the Calendar icon on the Dock you can settle for only blessing the framework.
- ```sudo bless --mount "$HOME/livemount/System/Library/PrivateFrameworks/CalendarUIKit.framework/" --setBoot --create-snapshot```


##### **CREDITS**

**_Jeremy Legendre_** Has made it possible to continue low-level system theming past macOS Big Sur
[https://github.com/jslegendre]()
[https://github.com/jslegendre/ThemeEngine/releases]()

**_Alex Zielenski_** One of my earlier partners in theming  - Maker of Mousecape and ThemeEngine
[https://github.com/alexzielenski/]()

**_Wolfgang Baird_** MacForge & PaintCan plugin
[https://github.com/w0lfschild]()

The path to the icon is courtesy of **_Paulo Freitas Valvator_** over at MacRumors Forums here:
[https://forums.macrumors.com/threads/changing-system-icons-on-big-sur.2243470/page-4?post=29648053#post-29648053]()

Paulo explains in the thread linked to, that you need to change the icon in the Assets.car in 2 places on your system.
However, my experience is that I only needed to change the actual ICNS file as in indicated in the Finder path above as I could not locate the icns file inside the Assets.car file.
