Photon
======

Organize your photos and videos by date in folders.

Photon is a simple command line tool for organizing photos and
videos in folders, and putting all photos and videos taken with
different cameras in one organized folder. It extracts date
and time of photos and videos (from filename, or image attributes,
or file modification time) and classifies them in folders (one
folder for each month).

Photon organizes this:

    new_photos/
    ├── 2014-12-17-224924.jpg
    ├── 2015-01-03-134015.jpg
    ├── 2015-01-03-134031.jpg
    ├── IMG 2014-10-24-211327.jpg
    ├── screenshots
    │   ├── Screenshot from 2014-12-30 20:43:02.png
    │   ├── Screenshot from 2014-12-30 20:46:25.png
    │   └── Screenshot from 2015-01-07 12:33:24.png
    └── VID 2014-10-24-211429.mp4

like this:

    organized_photos/
    ├── 2014
    │   ├── Oct
    │   │   ├── IMG 2014-10-24-211327.jpg
    │   │   ├── VID 2014-10-24-211429.mp4
    │   │   └── VID 2014-10-24-211429 PHOTON-VIDEO-PLACEHOLDER.jpg
    │   └── Dec
    │       ├── 2014-12-17-224924.jpg
    │       ├── Screenshot from 2014-12-30 20:43:02.png
    │       └── Screenshot from 2014-12-30 20:46:25.png
    └── 2015
        └── Jan
            ├── 2015-01-03-134015.jpg
            ├── 2015-01-03-134031.jpg
            └── Screenshot from 2015-01-07 12:33:24.png

or like this:

    organized_photos/
    ├── 2014
    │   ├── 10
    │   │   └── 24
    │   │       ├── 21:13:27.jpg
    │   │       ├── 21:14:29.mp4
    │   │       └── 21:14:29 PHOTON-VIDEO-PLACEHOLDER.jpg
    │   └── 12
    │       ├── 17
    │       │   └── 22:49:24.jpg
    │       └── 30
    │           ├── 20:43:02.png
    │           └── 20:46:25.png
    └── 2015
        └── 01
            ├── 03
            │   ├── 13:40:15.jpg
            │   └── 13:40:31.jpg
            └── 07
                └── 12:33:24.png

or ...


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

    IMPORTANT NOTE

    If you are not sure about what will happen after running the command, first use
    --dry-run flag, and if everything was ok, then run the command without --dry-run.

Suppose your directory structure is like this
(`organized_photos` is the directory containing your old photos organized by Photon.)

    .
    ├─ organized_photos
    ├─ new_photos
    └─ ...

For adding new photos (photos in `new_photos` folder) to your
organized photos, run:

    photon cp new_photos organized_photos

The above command **recursively copies** files from `new_photos` to `organized_photos`.
If you want to **recursively move** files instead of copying, run:

    photon mv new_photos organized_photos

Above commands use the default pattern for file paths (`{y}/{m} - {M}/{original_name}`).
You can use any pattern you wish. e.g. `{y}/{M}/{y}-{m}-{d} {h}:{mi}:{s}`. Note that this
pattern renames file names to `{y}-{m}-{d} {h}:{mi}:{s}`. I, personally use this command:

    photon mv new_photos organized_photos --jalali --chars fa --pattern "{y}/{m} - {M}/{y}-{m}-{d} {h}:{mi}:{s}"


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
      --pattern [PATTERN]  use PATTERN for file paths
                           default: "{y}/{m} - {M}/{original_name}"
                           example: "{y}/{m} - {M}/{y}-{m}-{d} {h}:{mi}:{s}"


Todo
----

* Write tests
* Improve extracting datetime from photos and videos


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
