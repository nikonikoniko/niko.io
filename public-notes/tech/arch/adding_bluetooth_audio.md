I really don't like using pulseaudio, so here is my bluetooth setup

that let's me switch between using it and not.

first the requirements:

```
yay -S bluez-alsa-git # renamed bluealsa
pacman -S bluetooth
pacman -S blueman # for the gui applet config
```

### switching between alsa devixes

I have a startup script in my home directory `startbluetooth.sh`

```
#/bin/bash
systemctl start bluealsa.service &
systemctl start bluetooth.service &
ln -sf /home/uer/.asoundrc-bluetooth /home/uer/.asoundrc &
alsactl restore
```

and another one to undo the changes `endbluetooth.sh`:

```
ln -sf /home/uer/.asoundrc-normal /home/uer/.asoundrc &
alsactl restore
```

these files will switch out the alsa config files for using bluetooth and normal alsa.

the contents of the `.asoundrc-normal` file is empty

here is `.asoundrc-bluetooth`:

```
defaults.bluealsa.service "org.bluealsa"
defaults.bluealsa.device "00:13:EF:FE:00:FD"
defaults.bluealsa.profile "a2dp"
defaults.bluealsa.delay 10000
defaults.bluealsa.mixer_device "blue"
pcm.btspeaker {
 type plug
  slave {
    pcm {
      type bluealsa
      #interface hci0
      device 00:13:EF:FE:00:FD
      profile "a2dp"
    }
  }
  hint {
    show on
    description "blue"
  }
}

# Instruct ALSA to use pcm.duplex as the default device
pcm.!default {
    type plug
    slave.pcm "btspeaker"
}

# tell ALSA to use hw:0 to control the default device (alsamixer and so on)
ctl.!default {
    type hw
    # A adapter en fonction de la config de reconnaissance
    # par Pi, il se peut que l'ordre ne soit pas le m  me
    card 0
}
```

switch out the device number for the device number found in the bluetooth connection gui.

use the gui to actually connect to the device.

The same config file with a little built in preamp:

```
defaults.bluealsa.service "org.bluealsa"
defaults.bluealsa.device "00:13:EF:FE:00:FD"
defaults.bluealsa.profile "a2dp"
defaults.bluealsa.delay 10000
defaults.bluealsa.mixer_device "blue"
pcm.btspeaker {
 type plug
  slave {
    pcm {
      type bluealsa
      #interface hci0
      device 00:13:EF:FE:00:FD
      profile "a2dp"
    }
  }
  hint {
    show on
    description "blue"
  }
}
pcm.softvol {
        type softvol
        slave {
                pcm 'btspeaker'
        }
        control {
                name 'Pre-Amp'
                card 0
        }
        min_dB -5.0
        max_dB 20.0
        resolution 6
}

# Instruct ALSA to use pcm.duplex as the default device
pcm.!default {
    type plug
    slave.pcm "softvol"
}

# tell ALSA to use hw:0 to control the default device (alsamixer and so on)
ctl.!default {
    type hw
    # A adapter en fonction de la config de reconnaissance
    # par Pi, il se peut que l'ordre ne soit pas le m  me
    card 0
}
```
