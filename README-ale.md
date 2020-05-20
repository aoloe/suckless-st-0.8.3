# st for ale

the latest tag  and the current master did not compile:

```
git checkout -b ale-2020 0.8.3
```

the `tar.gz` for 0.8.3 does compile.

## patches may 2020

### change target directory

```
diff --git a/config.mk b/config.mk
index 81e3e47..849b00a 100644
--- a/config.mk
+++ b/config.mk
@@ -4,7 +4,7 @@ VERSION = 0.6
 # Customize below to fit your system
 
 # paths
-PREFIX = /usr/local
+PREFIX = /home/ale/bin/st
 MANPREFIX = ${PREFIX}/share/man
 
 X11INC = /usr/X11R6/include
```

### solarized light

I could not apply the patch with 0.8.3 (it worked with 0.8.2).

The [no bad colors](https://st.suckless.org/patches/solarized/st-no_bold_colors-20170623-b331da5.diff) patch might or not be needed. (it does not seem to make a difference).

I could use the file created by pywal in a venv

- venv and pyinstall pywal
- `wal -l --theme base16-solarized` for applying the theme to all open terminal
- this might break all open terminals!
- `wal -s -t -l --theme base16-solarized` might create the `.h` file without applying the theme to the existing terminals
- copy `~/.cache/wal/colors-wal-st.h` to the `st` source directory.
- follow [this](https://github.com/dylanaraps/pywal/wiki/Customization#st) and
  - Remove all color definitions in your `config.h`
  - Remove the `const char *colorname[]` array
  - Include wal's export colors via: `#include "/home/<USER>/.cache/wal/colors-wal-st.h"` at the same place where you removed the colors definitions.

The archlinux article on [Getting solarized colors right with urxvt, st, tmux and vim](https://bbs.archlinux.org/viewtopic.php?id=164108) can be helpful (it helped me to get the correct commands in `vimrc`).

### one clipboard

trivial, manually applied.

allows a saner clipbaord management between terminal and GUI programs.

### visualbell

it applies correctly with

```
patch << ...diff
```

### hidecursor

The patch did not apply.

Manually applying and then it compiles.

Not applied. My cursor is small enough.

### inversescreen

- it does not exist anymore
- manually applying does not inverse the screen

### invert

do not apply this patch!

- i could not get the ctrl-x key to work
- applied without the `invert` function (always on)

### do not make bold lighter

do not apply this patch!

it breaks the solarized patch.

the solarized patch has its own fix for this.
