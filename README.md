kid's toy: Jukebox controlled by rfid cards

Materials used:
- raspberry pi 
- usb rfid reader acting as an USB keyboard.
- a set of compatible rfid cards

- when the rfid reader outputs a card code, the player checks if a filename starting with the code (and a dash) exists.  If so it starts playing it.

there are two special cards:
"key" unlock/lock the player
"stop" stop playing the current song
To identify these cards to the player, create files by those names and rename them to prefix them with the text generated by the rfid reader for those cards.

Dependencies/install:

The default login agetty process on the first video console is replaced with the player (note you can still login with keyboard if you switch to another video console eg. with ctrl-alt-f2):

place `play.py`, `play.service` in `/home/pi`

run:

    apt-get install sox alsamixer
    sudo install -m 644 play.service /etc/systemd/system/play.service
    sudo systemctl daemon-reload
    sudo systemctl mask getty@tty1.service
    sudo systemctl enable play.service
    sudo systemctl start play.service

use `raspi-config` to enable playback to jack
use `alsamixer` to set an acceptable volume
make sure to shut down correctly to have alsa save the volume levels.
