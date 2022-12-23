# Guide to updating vrelay

Throughout this tutorial, we will be liberally using [JPEXS](https://github.com/jindrapetrik/jpexs-decompiler/releases).

## What needs to be updated?

Here's a list of what we need to do.

1. Autonexus (bullets/tiles/AoE)
4. Adding proxy server in `Valor.swf`.
3. Check for new anticheat in `Valor.swf`.
4. Caveats + Useful ideas to think about

## How to update each step?

Start by opening `Valor.swf` in JPEXS.

### 1. Autonexus

If you look in `vrelay/bin`, you will see four `.pkl` files. Each `.pkl` contains information on AoE, bullet, name of enemy, and tile damage, respectively. We need to update these.

First, we will prepare the data.

#### Bullets/tiles:

1. In JPEXS, right-click `binaryData` -> `Export selection`. Click OK.
2. ** Export in the folder `vrelay/updater`. ** You MUST export in `vrelay/updater` or the parsers will not know where the data is.

Note: these XMLs contain all the bullet/tile data.

#### AoEs

This is where the `vrelay/logs` folder comes into handy. I have written some scripts to parse and analyze all the logs and save all the data in `bin/AoeDictionary.pkl`.

1. Copy all of your logs.
2. Create a new folder in `vrelay/updater/userLogs`. There is a database of logs collected from many people. 
3. Paste all of your logs into the new folder you just created.

#### Making the `.pkl` files

1. Run `vrelay/updater/parsers/updater.bat`. These scripts will analyze the AoE/bullet/tile data you just prepared.

Autonexus is now updated.

## Adding proxy server

1. Navigate to the file `kabam/rotmg/servers/control/ParseServerDataCommand.as`. 
2. Click `Edit ActionScript`.
3. Copy paste the code in `vrelay/updater/kabam-rotmg-servers-control-parseserverdatacommand.as` into the editor.
4. Save the `.swf`.


# Caveats
1. The more monsters you see, the more complete and better autonexus is at predicting AoE's. This is because the log files will be more likely to capture various AoE's
2. Learn a bit of Python. This will help you understand better what is happening.
3. The AoE script starts with raw logs and spits out a nice dictionary. Read the comments in `AoESerializer.py` to understand the algorithm being used to analyze this data.
    - The algorithm is not perfect but it works well in practice.
