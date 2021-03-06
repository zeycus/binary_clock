****************************
Truly Binary Clock in Python
****************************


Overview
========

There are many `binary clocks <https://en.wikipedia.org/wiki/Binary_clock>`_ and watches advertised on the Internet, it is even possible to actually buy wrist binary watches,
for instance in `Ledwatchstop <https://www.ledwatchstop.com/store/binary-c-5.html>`_. 
However, as far as I know they are only binary on the surface, measuring the time of the day 
conventionally, in hours + minutes. It's just that those two numbers are somehow represented in binary.

Module **binary_clock** provides an implementation of what I consider a truly binary clock.
The first bit stands for the half of the day, 12 hours. The second, for the a quarter of a day, 6 hours, and so on.
Each bit stands for an interval that is the half of the previous.

For instance, 11010000 represents 12 + 6 + 1.5 = 19.5, which means 7:30 PM.

Another way to see it is that 0.11010000 is the fraction of the day passed, in binary. So, 0.11010000 = 13/16 of a day.


Modes
=======

Two modes are provided. The simplest option is to use flat colors, each bit is shown with a square of that color. The binary clock then
looks like this:

.. image:: images/animation_flat.gif
   :scale: 100 %
   :alt: Binary clock with flat bits
   :align: center

Bits should be read left-to-right, top-to-bottom. With this 4x4 format, it is suitable to stand as one icon more on the desktop.
   
If you want to get fancy, the second mode allows you to choose any two equal-size images, one for on-bit and another for off-bit, getting something like:
   
.. image:: images/animation_image.gif
   :scale: 70 %
   :alt: Binary clock with images
   :align: center


   
Usage
===========

All the code is in file ``binclockWrapper.py``, launched by command line script ``binclock.py``. The arguments supported are

``geometry``
  mandatory argument of the form axb, where a and b are integer numbers. It provides the size of the grid of bits.

``offset``
  string that provides the initial offset from the bottom-right corner of the screen. For instance, '-1-43' is 1 pixel to the left
  and 43 upwards. Clocks are draggable, you can move them once created.

``side`` and ``color``
  For the *flat* mode.
  In the latter case, ``side`` is the number of pixels per side, and ``color`` a string in format '#rrggbb' in hexadecimal.
  For instance, yellow is '#ffff00'.

``imageon`` and ``imageoff``
  Strings for filenames, for the *image* mode. If provided, options ``side`` and ``color`` are ignored.

``borderwidth``
  is the width of each bit inside its frame, in number of pixels.

``bgcolor``
  is the color of the frame, in '#rrggbb' format.

``persistent``
  is a flag that, if present, forces the clock to always stay on top of other windows.

  
---------
Examples
---------

Flat mode:

.. code-block:: bash

  binclock --color=#30a0ff --side=10 --borderwidth=2 --bgcolor=#808080 --geometry=4x4 --persistent

Image mode:

.. code-block:: bash
  
  binclock --imageon=light_green_button.jpg --imageoff=dark_green_button.jpg  --borderwidth=3 --bgcolor=#808080 --geometry=1x12

  

Observations
============

The blinking frequence of each bit is twice that of the previous bit. With 16 bits, the last one stands for 2^-16 days, more or less 1.318 seconds.
So, 16 bits is the closest you can get to the typical hours + minutes + seconds watch. If the value provided for ``geometry`` contains too many bits:

    * The consumption of CPU time will be noticeable

    * The computer/screen might not be fast enough to refresh bits with the speed that would be required.

In tests I performed, that limit of reasonable behaviour seems to be around 22 bits, but there seems to be little
point in using that many.


  

Collaboration
=============

You may wish to improve or add features, in that case you are more than welcome, feel free to contact me at zeycus@gmail.com.

