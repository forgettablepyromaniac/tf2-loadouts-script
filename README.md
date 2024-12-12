# junior's loadouts script

Loadout specific settings and a resup bind that knows which loadout you're on.
Edits by FP

## Features

- single resup key that always respawns you on the right loadout
- loadout specific settings
- remembers which loadout you have active on each class,
  even after you restart TF2

# Resup bind _aka b4nny bind_
lets you resupply while in spawn without needing to touch the fridge/cabinet.
Unlike switching classes, it preserves all of your buildings, stickies
and ubers (but not stored crits, heads or banner charges).  

## Setup

1. Download init.cfg, put it in `tf/cfg/loadouts/`. If the folder doesn't exist, create it.
2. Add `exec loadouts/init` to your `autoexec.cfg`
3. Add `loadouts.<class>` **at the end** of each of your `<class>.cfg`  

   Replace `<class>` with actual class names:
   `scout`, `soldier`, `pyro`, `demoman`,
   `heavyweapons`, `engineer`, `medic`, `sniper`, `spy`

4. Bind your keys
  
   `loadouts.A`, `loadouts.B`, `loadouts.C`, `loadouts.D` for switching loadouts  
   `loadouts.resup` to resupply 

   Do this in your `autoexec.cfg` or wherever you have your binds.

   ```
   bind F1 loadouts.A
   bind F2 loadouts.B
   bind F3 loadouts.C
   bind F4 loadouts.D
   bind ALT loadouts.resup
   ```

## Loadout specific settings

When changing to loadout _X_, the script calls corresponding `loadout.cfg.X` alias.
You can set these aliases to execute arbitrary commands when changing lodouts.

If you want to set these per class in your `<class>.cfg`, you need to
do so **before** the `loadouts.<class>` line.
If you want to set them globally, do so in your `autoexec.cfg` **after**
the `exec loadouts/init` line.

Don't forget to reset these aliases (and affected settings) for other classes,
otherwise their values will carry over.

Your `medic.cfg` could look something like this.
```
// insert generic medic script up here.

alias loadouts.cfg.A "exec uber; say_team running uber"
alias loadouts.cfg.B "exec kritz; say_team running kritz"
alias loadouts.cfg.C "exec quickfix; say_team running quickfix"
alias loadouts.cfg.D  // no settings for D

loadouts.medic
```

## FAQ

### There's a delay between when I press the key and respawning.
That's normal. Happens with all resupply binds. You should press it
(or spam it) right before you enter spawn.

### Why does `loadouts.<class>` have to be at the end?
It doesn't. But anything that comes after it overrides
the `loadouts.cfg.X` settings. If you are sure you're not breaking
anything, you can put it anywhere you like.

### Doesn't it break when item servers are down?
Yup.

### This won't function at all!!
If you’re using mastercomfig, you need to place some of your config-related files in `tf/cfg/app/(config).cfg` instead.

mastercomfig manages its own config files that are injected at runtime.
These files don’t physically appear in the filesystem,
but the game treats them as if they do, overwriting any custom ones you’ve added.

To fix this, make sure to put your config files in the `tf/cfg/app/` folder.
For example, instead of: `tf\cfg\autoexec.cfg`, Place it here: `tf\cfg\app\autoexec.cfg`
Do the same for class-specific configs: `tf\cfg\app\<class>.cfg`

I found this out [here](https://github.com/jooonior/tf2-loadouts-script/issues/15#issuecomment-2539331556), lmao.
