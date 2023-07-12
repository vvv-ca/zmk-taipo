# ZMK Taipo Layout Firmware

This repo contains the [ZMK](https://zmkfirmware.dev/) firmware for the Taipo layout.
The official description of the layout can be found on the [Inclusive Keyboards Taipo Page](https://inkeys.wiki/en/keymaps/taipo).

## Supported Devices

- Ferris Sweep (aka cradio)
- Corne (untested)

## Usage

- Navigate to the [Github Actions](https://github.com/dlip/zmk-taipo/actions) tab and select the latest build
- In the artifacts section download firmware.zip
- Unzip firmware.zip
- Put your device into bootloader mode
- Copy the appropriate .uf2 file to your device

## Layout

This configuration has some modifications from the original layout:

- Fn layer key switched to 'insert'
- Uses extra keybindings which use both thumb keys together.

```
Input Output Inner Outer Both
#---  r      R     >     Print Screen
----

-#--  s      S     }     Brightness Up
----

--#-  n      N     ]     Brightness Down
----

---#  i      I     )     Play/Pause
----

----  a      A     <     Next Track
#---

----  o      O     {     Volume Up
-#--

----  t      T     [     Volume Down
--#-

----  e      E     (     Previous Track
---#

----  c      C     1     F1
-#-#

----  u      U     2     F2
-##-

----  q      Q     3     F3
#--#

----  l      L     4     F4
##--

--##  y      Y     5     F5
----

-#-#  f      F     6     F6
----

-##-  p      P     7     F7
----

#-#-  z      Z     8     F8
----

##--  b      B     9     F9
----

----  h      H     0     F10
--##

----  d      D     @     F11
#--#

#--#  g      G     #     F12
----

#---  x      X     ^
--#-

---#  k      K     +
-#--

-#--  v      V     *
---#

--#-  j      J     =
#---

#---  m      M     $
---#

---#  w      W     &
#---

-#--  /      \     |
--#-

--#-  -      _     %
-#--

#---  ;      :
-#--

---#  ?      !
--#-

--#-  ,      .     ~
---#

-#--  '      "     `
#---

-###  Tab    Del   Insert
----

----  Enter  Esc   AltGr
-###

#---  Gui    Right PgUp
#---

-#--  Alt    Up    Home
-#--

--#-  Ctrl   Down  End
--#-

---#  Shift  Left  PgDn
---#
```

## Local Development

### Docker

#### Setup and build

```
scripts/docker-image.sh
scripts/docker-dev.sh
west init -l config
west update
west zephyr-export
west build -p -s zmk/app -b nice_nano_v2 -- -DSHIELD="cradio_left" -DZMK_CONFIG="$PWD/config"
```

The firmware file will be `build/zephyr/zmk.uf2`

#### Resume after quitting

```
  docker start -i zmk-taipo-dev
```

#### Clean up

```
  docker rm zmk-taipo-dev
```
