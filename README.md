# onionscraper
A script to scrape artwork for OnionOS on the Miyoo Mini and Mini+. The actual scraping is done with Skyscraper.

### Requirements
- bash (Linux, MacOS, Cygwin...)
- Skyscraper: [Lars Muldjord](https://github.com/muldjord/skyscraper)'s original or [Detain](https://github.com/detain/skyscraper)'s more recent fork.
- xmlstarlet (optional)

### Installation
soon

### Configuration
.skyscraper/config.ini
```
[main]
inputFolder="/PATH_to_YOUR_ROMS"
cacheMarquees="false"
cacheTextures="false"
relativePaths="true"
gameListBackup="false"
nameTemplate="%t"
frontend="emulationstation"

[screenscraper]
userCreds="USERNAME:PASSWORD"
```

### Usage
```
Usage: onionscraper [OPTIONS] [PLATFORMS]
Scrape artwork for new ROMs or for given systems. Helps mananaging artwork.
options:
  -a --all:    check all platforms instead of just the ones with new ROMs.
  -c --clean:  remove images for deleted games.
  -d --dry-run with clean, find but don't delete images.
  -i --import: import manually added assets.
  -s --skip:   skip existing output files.
  -h --help:   this help.
```

Called without parameters, `onionscraper` will find new ROMS added since the previous run of the script
and scrape the artwork. A file called `miyoogamelist.xml` is generated or updated so device will show the game
titles instead of the file names. If `xmlstarlet` is installed, unnecessary information in this file 
will be removed.

The first invocation of `onionscraper` can take a while as all the ROMs are scraped.

You can provide your own images for the artwork. See below how to provide it. To use your newly added images, call the script with `-i` or `--import`.

If called with `-a` or `--all`, all the systems will be scanned instead of just the systems with new games.


### Importing local images
The artwork is generated from the *screenshot* and *wheel* assets.

See [Skyscraper's documentation](https://github.com/muldjord/skyscraper/blob/master/docs/IMPORT.md) on import for the details. By default, Skyscraper looks for images to import in `~/.skyscraper/import`.
Inside this directory, my preference is to store my images per platform and then per asset type. For example:
```
~/.skyscraper/import/snes/screenshot/Good Game (Europe).png
~/.skyscraper/import/wonderswan/screenshot/Another Game (Japan).png
```
Note that here the Skyscraper platforms are used, not the Miyoo system directories. So it is `snes` and not `SFC`, `wonderswan` and not `WS`, etc...
