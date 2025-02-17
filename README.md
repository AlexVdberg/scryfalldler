# scryfalldler
Simple (fast and probably *bad* coded) php client automated script for download and zip card images using the open [scryfall.com](http://scryfall.com) API site ready for XMage.

This script is a simply php cli coded. I wanted to practice a bit with php cli scripts and this is what I made. With php we can take advantage of expanded php multi-platform, client executed (not web server, to avoid requests and filesize limitations), easy curl (http download) and zip tools.

Use [Issues](https://github.com/nachazo/scryfalldler/issues) for feature request or bugs.

Don't forget to support [scryfall.com](http://scryfall.com).

## How to run
You only need **php** 5.3+ (instaled in your system or uncompressed, for example from [php downloads page](http://php.net/downloads.php) or LAMP folder - note: **no** web server required, only php) with **curl extension enabled**. Normally comes installed and enabled in most lamps or similar. If not, for Debian based GNU/Unix like Ubuntu, you simply can do it with `sudo apt install php-curl`. For Windows, search over there (could be done just editing two lines in php.ini file) :P

So, just execute command and place resultant zip in your XMage images folder. For tokens you can drag&drop to TOK.zip file.

Btw, script doesn't need php-zip extension, I'm using built-in phar to compress in zip (one requirement less) and in my tests result size is the same (phar bundles with php 5.3+).

Don't forget to test set results on XMage "Viewer". There you can see bad or errored named cards. With common Zip filemanagers (like 7Zip or WinRAR) you could edit the name with it for fix.

### GNU/Unix based
Download the script where you want, for example using:
```cmd
> wget https://raw.githubusercontent.com/nachazo/scryfalldler/master/scryfalldler
```
And then simply run it with the desired options (this is a test command):
```cmd
> php scryfalldler -l
```
This example will show a list with the avaiable sets. Bellow you have some example commands.

If you don't have php path configured in file system, you could invoke pointing php binary file, for example using:
```cmd
> /etc/bin/php scryfalldler -l
```
Also, if you want, you can give execute permissions with `chmod +x scryfalldler` to use without "php" word in the commands, just `scryfalldler` (or depending your system `./scryfalldler`). Depending how you saved the file, maybe you need to convert line endings with `sed -i s/\\r//g scryfalldler`.

### Windows based
Download the script where you want, save the path to a file or, for example, using Windows PowerShell (<kbd>Win</kbd> + <kbd>r</kbd>, then `powershell`):
```cmd
> wget https://raw.githubusercontent.com/nachazo/scryfalldler/master/scryfalldler -OutFile scryfalldler
```
And then simply run the command with the desired options (this is a test command):
```cmd
> php scryfalldler -l
```
This example will show a list with the avaiable sets.

> *Note*: If you see weird symbols instead colors in the console, it's because [a problem with Windows ANSI encoding and php version](https://github.com/symfony/symfony/issues/19520). With lastest versions you will avoid it. Anyways, the image download works aswell :)

If you don't have php path configured in file system, you could invoke pointing binary php.exe file, for example using:
```cmd
> C:\myPhpFolder\php scryfalldler -l
```

## Example commands
Of course you can combine parameters, also using short or large reserved words, all listed in "Help" section (or type `php scryfalldler`).
* This will download "Commander 2017" set cards (in large size) and zip to "C17.zip" in base folder:
  * `php scryfalldler -s c17`
* This will download "Commander 2017" set cards and zip to "C17.zip" in specified folder:
  * `php scryfalldler -set c17 -f /home/user/xmage/myImages`
* This will download "Commander 2017" cards art crop image set:
  * `php scryfalldler -set c17 -size art_crop`
* This will download "Commander 2017" set cards behind proxy:
  * `php scryfalldler -s c17 -p http://myproxy:8888`
* This will download "Commander 2017" card images from Wizards Gatherer:
  * `php scryfalldler -s c17 -z gatherer`
* This will download "Commander 2017" tokens and zip into a subfolder named "C17", you could drag&drop to TOK.zip:
  * `php scryfalldler -set tc17 -r C17`
* This will read each line of "My deck file.text" and search in Scryfall for cards, then save that in the script format, in a zip "MYDECKRESULT.zip". Useful for common deck files, for example:
  * `php scryfalldler -file "My deck file.txt" -r MYDECKRESULT`
* This will download "Future Sight" set from Gatherer and generate correctly with "FTS.zip" name:
  * `php scryfalldler -g "Future Sight" -r FTS`
* This will download "Exodus" set from Gatherer:
  * `php scryfalldler -g exodus`
* This will download card images from official Wizards product set images, this case for Dominaria. Missing images would be taken from Gatherer:
  * `php scryfalldler -u https://magic.wizards.com/en/products/dominaria/cards -r DOM`
* This will download token images from official Wizards product images, this case for Dominaria. As it have not names, could be unnamed (you may rename):
  * `php scryfalldler -u https://magic.wizards.com/en/articles/archive/card-preview/tokens-dominaria-2018-04-12 -r TOK`

  
## Changelog

* **1.4.2** (21/05/20):
  * Fixed Adventures for set ELD. Made by @huwwevans.
* **1.4.1** (15/06/18):
  * Small fix for cards with foil versions causing bad exporting.
* **1.4** (27/04/18):
  * Added "-g" option for download from Wizards Gatherer without taking any info from Scryfall. Doing it searching by set name.
  * Added "-u" option for download from Wizards official set site card page. Empty cards comes from Gatherer. Also tokens, but "unnamed". Not works as good as Scryfall, needs some post-renaming, but usefull in early launched sets.
* **1.3.3** (02/04/18):
  * Configured error reporting for avoid showing in output high number of warnings and so on. Now only important errors will be shown.
* **1.3.2** (13/03/18):
  * Improved the new file list option. Now you could specify the set you want for the card edition with "card|set" (i.e: Opt|INV) (useful for lands also you can use collector number with #, i.e. Forest|bfz#273). Also, can read the XMage .dck format.
* **1.3.1** (12/03/18):
  * Fixed error saving cards with " in the name. Until now, these cards doesn't download.
  * Corrected version naming.
* **1.3** (12/03/18):
  * Added optional feature for download card images from a file list (deck file, for example).
* **1.2** (12/03/18):
  * Fixed error saving split cards (the cards with "//"). Until now, these cards doesn't download.
  * Fixed error saving cards with ":" and " * " in name. Replaced by blank, like XMage does. As strange chars in some systems, until now it caused that images with that doesn't download.
  * Added option (-x, -ext) for force the image extension for the cards.
* **1.1** (09/02/18):
  * Fixed a relevant bug with basic land naming.
* **1.0** (10/01/18):
  * Initial release.

## Help
Command `php scryfalldler -h` shows:
```yaml
Usage:
  php scryfalldler [arguments] 

Arguments: 
  All arguments also accept "--". 
    -h, -help		Shows help (this info). 
    -v, -version	Show version from your downloaded script.
    -l, -list		List avaiable sets for download with codes from Scryfall. 
    -s, -set		Launch download cards operation from the specified set from the site. 
    -z, -size		The size for downloaded images ("image_uris" from Scryfall API).
                        Special value "gatherer" downloads Wizards Gatherer image if avaiable. 
                         Default value: large. 
                         Possible values: small, normal, large, png, art_crop, border_crop, gatherer.  
    -u, -url		Download a set from the Wizards official site URL.
                        Usefull for new spoilers and for tokens pages. 
    -g, -gatherer	Download a set from Wizards Gatherer searched by name. 
    -f, -folder		Destination folder for the zip file (not tested with relative ones). 
    -r, -force		Force zip and inside folder name (for tokens download, for example).
    -d, -debug		With this, script only show messages but not download or create folder. 
    -t, -test		Test your connection with Scryfall. 
    -p, -proxy		Set proxy for connections (format http://proxy:port).
    -n, -no-check	By default, script check for updates each execution (requesting to GitHub).
                        A message will warn you on new versions. You can avoid it with this option.
    -x, -ext		Extension for card images. Instead .jpg (default value) that XMage uses,
                        you could force what will be used, for example "png" 
                         Default value: jpg.
    -i, -file		Optional file location, with cards-per-line for export a concrete group of
                        cards (a deck for example - allows XMage .dck format) like a set.
                        You could specify optionally the set for card edition (card|set) and collector
                        number (card|set#collnum) (for example, for lands). If not, last published
                        edition of the card will be downloaded. 

Site: 
  https://github.com/nachazo/scryfalldler 
```

<p align="center"><img src="https://i.imgur.com/I7QEYF6.gif" data-canonical-src="https://i.imgur.com/I7QEYF6.gif" width="500" /></p>
