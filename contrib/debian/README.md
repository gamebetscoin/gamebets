
Debian
====================
This directory contains files used to package gamebetsd/gamebets-qt
for Debian-based Linux systems. If you compile gamebetsd/gamebets-qt yourself, there are some useful files here.

## gamebets: URI support ##


gamebets-qt.desktop  (Gnome / Open Desktop)
To install:

	sudo desktop-file-install gamebets-qt.desktop
	sudo update-desktop-database

If you build yourself, you will either need to modify the paths in
the .desktop file or copy or symlink your gamebetsqt binary to `/usr/bin`
and the `../../share/pixmaps/gamebets128.png` to `/usr/share/pixmaps`

gamebets-qt.protocol (KDE)

