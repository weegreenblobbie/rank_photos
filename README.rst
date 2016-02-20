Photo Ranking With Elo
======================

.. hyper link references

.. _`Elo Ranking System`: http://en.wikipedia.org/wiki/Elo_rating_system
.. _`exifread`: https://pypi.python.org/pypi/ExifRead


What is this?
-------------

This is a tool that uses the `Elo Ranking System`_ written in Python using:
- Matplotlib
- Numpy
- exifread

Features:
- Persistent state from execution to execution so you can pickup where you left off
- Auto image rotation that the camera recored in the EXIF meta data


Install dependencies
--------------------

Use your system's package manager to install Numpy & Matplotlib if you don't
already have them installed.

Next, you can use pip to install the EXIF image reader package `exifread`_:

.. code-block:: bash

    pip install exifread --user


How to rank photos
------------------

Once you have to dependencies installed, run ``rank_photos.py`` on the command
line passing it the directory of photos.

.. code-block:: bash

    ./rank_photos.py --help
usage: rank_photos.py [-h] [-r N_ROUNDS] [-f FIGSIZE FIGSIZE] photo_dir

Uses the Elo ranking algorithm to sort your images by rank. The program reads
the comand line for images to present to you in random order, then you select
the better photo. After N iteration the resulting rankings are displayed.

positional arguments:
  photo_dir             The photo directory to scan for .jpg images

optional arguments:
  -h, --help            show this help message and exit
  -r N_ROUNDS, --n-rounds N_ROUNDS
                        Specifies the number of rounds to pass through the
                        photo set
  -f FIGSIZE FIGSIZE, --figsize FIGSIZE FIGSIZE
                        Specifies width and height of the Matplotlib figsize
                        (20, 12)

For example, iterate over all photos three times:

.. code-block:: bash

    ./rank_photos.py -r 3 some/path/to/photos

After the number of rounds complete, `ranked.txt` is written into the photo dir.


Ranking work is cached
----------------------

After completing N rounds of ranking, a file called ``ranking_table.json`` is
written into the photo dir.  The next time ``rank_photos.py`` is executed with
the photo dir, this table is read in and ranking can continue where you left
off.

You can also add new photos the the directory and they will get added to the
ranked list even though they weren't included previously.


Example
-------

Suppose there is a dir containing some photos:

.. code-block:: bash

    ls -1 ~/Desktop/example/
        20160102_164732.jpg
        20160109_151557.jpg
        20160109_151607.jpg
        20160109_152318.jpg
        20160109_152400.jpg
        20160109_152414.jpg
        20160109_153443.jpg

These photos haven't been ranked yet, so lets ranking, 1 round:

.. code-block:: bash

    ./rank_photos.py -r 1 ~/Desktop/example/

Example display:

.. image:: screenshot.png
