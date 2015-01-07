Photon
======

Organize your photos and videos by date in folders.

Photon is a simple command line tool for organizing photos and
videos in folders, and putting all photos and videos taken with
different cameras in one place ordered by time. It extracts date
and time of photos and videos (from filename, or image attributes,
or file modification time) and classifies them in folders (one
folder for each month).

It organizes this:

    new_photos/
    ├── 2014-12-17-224924.jpg
    ├── 2015-01-03-134015.jpg
    ├── 2015-01-03-134031.jpg
    ├── IMG 20141214-144724.jpg
    ├── IMG 20141215-173654.jpg
    ├── Screenshots
    │   ├── Screenshot from 2014-12-30 20:43:02.png
    │   └── Screenshot from 2014-12-30 20:46:25.png
    └── VID 20141214-144938.mp4

like this:

    organized_photos/
    ├── 2014-12
    │   ├── 2014-12-14 14:47:24.jpg
    │   ├── 2014-12-14 14:49:38.mp4
    │   ├── 2014-12-14 14:49:38 PHOTON-VIDEO-PLACEHOLDER.jpg
    │   ├── 2014-12-15 17:36:54.jpg
    │   ├── 2014-12-17 22:49:24.jpg
    │   ├── 2014-12-30 20:43:02.png
    │   └── 2014-12-30 20:46:25.png
    └── 2015-01
        ├── 2015-01-03 13:40:15.jpg
        └── 2015-01-03 13:40:31.jpg


Why?
----

I needed a simple tool for organizing photos taken by camera,
and sorting all photos taken with different cameras in one place
ordered by time. The simplest approach for organizing was using
folders. Also, there wasn't any photo organizer app for linux which
could organize photos using Persian calendar (Maybe there is a way
to do it in KDE, but I don't use KDE.) So I wrote this simple
Python 3 script.


Installation
------------

Photon needs `Pillow` Python library. After installing `Pillow`,
add following line to your `~/.bashrc` file.

```bash
alias photon="python3 PATH/TO/photon"
```


Getting Started
---------------

Suppose your directory structure is like this
(`organized_photos` is empty at the beginning.)

    .
    ├─ organized_photos
    ├─ new_photos
    └─ ...

For adding new photos (photos in `new_photos` folder) to your
organized photos, run:

    photon cp new_photos organized_photos

The above command copies files from `new_photos` to `organized_photos`.
If you want to move files instead of copying, run:

    photon mv new_photos organized_photos


Usage
-----

    usage: photon [-h] [--jalali] [--chars {fa,en}] [--dry-run] [--pattern [PATTERN]]
                  CMD TARGET ORG_DIR

    positional arguments:
      CMD                  {mv,cp}
                           mv: move files to ORG_DIR
                           cp: copy files to ORG_DIR
      TARGET               file or folder to be organized
      ORG_DIR              folder to save organized files

    optional arguments:
      -h, --help           show this help message and exit
      --jalali             convert dates to Persian (use Persian dates in organized file names)
      --chars {fa,en}      use Fa/En characters for digits in file names (default: en)
      --dry-run            do not copy or move files. just print what will happen
      --pattern [PATTERN]  use PATTERN for file names
                           default: {y}-{m}-{d} {h}:{mi}:{s}


Warning
-------

    This program recursively RENAMES and (when used with "mv" command) MOVES files
    located in TARGET, and uses the pattern specified by --pattern for
    new file names. So, if you have a photo named "important-20140705-154547.jpg",
    its name changes to something like "2014-07-05 15:45:47.jpg" and the
    "important" part is removed from file name.

    If you are not sure about what will happen, first use --dry-run flag, and if
    everything was ok, then run the command without --dry-run.


Todo
----

* Write tests
* Add other folder structures for organizing (e.g. YEAD/MONTH/ instead of YEAR-MONTH/)


Want to contribute?
-------------------

Feel free to fork Photon and start contributing.


License
-------

Photon is licensed under GNU GPLv3.


Projects used in Photon
-----------------------

* https://github.com/mjnaderi/Jalali.py
* https://github.com/i-tu/Hasklig
* Pillow
