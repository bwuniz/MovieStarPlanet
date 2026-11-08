# MSP2016

A self-contained installer for running the 2016 MovieStarPlanet client on PC, completely offline. Partially functional. Everything it needs is inside the installer: the server, Node, MongoDB, the Flash plugin and the game shell. It does not phone home, and it works without Wi-Fi.

This is an unofficial, fan-made reimplementation of the game's backend. It talks
to the original 2016 client; it contains no original server software. MovieStarPlanet
is not affiliated with it.

## You will need

- Windows 10 or 11, 64-bit
- About 1.5 GB free disk
- Administrator rights, for the installer

## Install

Run `MSP2016.exe` from releases, and follow it through. It installs to
`Program Files\MSP2016`, adds a shortcut, and writes two entries to your hosts
file so the client's hardcoded hostnames resolve to this machine:

```
127.0.0.1  upload.alpha.moviestarplanet.com
127.0.0.1  cdn.alpha.moviestarplanet.com
```

Those two lines are removed again on uninstall. If you'd rather not have the
installer touch the hosts file, run it, then add them yourself afterwards.

Windows Defender SmartScreen will complain, because this is an unsigned build
from nobody in particular. "More info" then "Run anyway".

## Starting it

Use the shortcut generated on your desktop. It starts the server and opens the game window. Give it up to
about a minute the first time - it builds its database and unpacks the item
catalog before the loading bar moves.

If you want to start it by hand instead:

```
cd "C:\Program Files\MSP2016"
node server\index.js
```

The server listens on ports 80, 443, 1600, 1935 and 5222. If a firewall prompt
appears, allow it on a private network only - nothing here needs to accept
connections from other machines, and you can block it publicly without any effect
on gameplay.

## Logging in

Two accounts exist from the start, the game's own anchor characters
Passwords are: npc123

Use one of them, or register your own
normally and you can make as many as you like.

Do not expose these ports to a network or the internet.

## One thing to do once

The client fetches a few assets over https from a host that this installer
redirects to your own machine, using a self-signed certificate. Open

```
https://upload.alpha.moviestarplanet.com
```

once in the shipped shell, accept the certificate warning, and you won't see it
again. Skip this and some images and assets will probably fail to load - 
which is an annoying thing to debug.

## Playing

Working: the clothing, diamond and room shops; the dressing room and saving
looks; friends, requests and chat including chat rooms; guestbook and activity
feed; forums with polls; making movies; pets; gifting; free VIP and diamond purchases; 
the fame wheel; etc.

## Currently not working

- In the looks window the detail card and the comment list keep placeholder
  text ("MyLook Name", "Friend Name", "3. okt 2010"). The look itself renders and
  comments do save. This is inside the original client, not the server.
- Room decorations you buy don't stay placed. Wallpaper and floor do save.
- The artbook creator's clipart tabs are empty; the art isn't distributed with
  this. Pages still save and open. (I believe)
- The YouTube tab is empty. There's no external video service behind it.
- You currently cannot watch movies or rate them. All of these issues will be later fixed

## Your data

Everything stays on your machine, in a local MongoDB instance the installer
bundles. Uninstalling removes the program; your game data lives under the
install directory and is not uploaded anywhere, ever. because there is nowhere
to upload it to.

## Uninstall

Through Windows' normal "Add or remove programs". It removes the shortcut, the
hosts entries and the program folder. Delete the folder afterwards if you also
want the database gone.
