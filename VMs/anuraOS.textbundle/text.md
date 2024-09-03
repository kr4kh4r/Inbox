anuraOS
-----------------------------------------------------------


What is AnuraOS?​

An entirely local browser "OS" and development environment with complete graphical linux emulation, visually based on chromiumOS. See a demo here, fully in your browser.

NOTE
Due to numerous issues with Firefox's implementation of certain web standards, it is not supported on Anura. Please use a chromium-based browser or you will have a significantly diminished user experience. Safari is also fully compatible, as long as you have MacOS Sonoma, or iPadOS/iOS 17 or later.
Anura uses the features of a progressive-web-app to make its environment work fully offline, providing a virtual filesystem (synced with the linux emulator), a code editor, and a modular and extensible app system. You can even edit Anura's code live while inside of it!

Anura shows as more of a proof-of-concept with what's possible on the modern web rather than an actual product. However, it proves useful in many actual cases and is a useful educational tool.

What can AnuraOS do?​

Run linux GUI apps from a terminal
Development

INFO
Anura will not build on Windows. Please use a Linux VM or WSL
Easy Install (When in a codespace)​

==Run bash codespace-basic-setup.sh==
NOTE
If you are not in a codespace skip to the regular installation steps. This does NOT build RootFS.
Installation​

Make sure you have rustup and run the command: rustup target add wasm32-unknown-unknown
You also need to have a C compiler, inotifytools and a decent version of java installed
Clone the repository with git clone --recursive
Then, make all
NOTE: You can use make all -B instead if you want to force a full build.
Building ROOTFS​

Make sure you have Docker installed and running.
Run make rootfs
Make sure to add yourself to the Docker group using usermod -a -G docker $USER
(Special Use Case) In the event that you should need to override/manually add the initrd and kernel, remember to keep track of the file names of initrd and vmlinuz in build/images/debian-boot/. Then, copy them to the Anura root directory and rename them to initrd.img and bzimage respectively.(See the extended instructions.)
Running Anura​

You can run anura with the command

make server

Or, run authenticated with

cd server
npm start -- --auth

After Installation​

NOTE: Anura uses recent web technologies, and is unstable in Gecko. Chromium is strongly recommended as it has seen the best results.

If you started the server, Anura should be running at localhost:8000.
Documentation​

Still being written. (See the current index of documentation)

Security​

See SecurityMD for reporting instructions.

Credits​

AnuraOS is created by Mercury Workshop. Linux emulation is based off of the v86 project
Edit this page
Previous
Alu
Next
Holy Unblocker LTS
Documentation
Get Started
Guides
Web Proxies
Exploits
Services
Anura OS
Holy Unblocker
Nebula Proxy
webretro
Alu
Kazwire
Ludicrous
Radon Games
Totally Science
AnuraOS
Archived
Incognito
Hypertabs
Corrosion Proxy
Alloy Proxy
PyDodge B
Greenlime
P2
Community
Mercury Workshop
Discord
Twitter
Copyright © 2024 Titanium Network