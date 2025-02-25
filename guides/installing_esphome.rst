Installing ESPHome Manually
===========================

Windows
-------

Download Python from `the official site <https://www.python.org/downloads/>`_.

.. figure:: images/python-win-installer.png
    :align: center
    :width: 75.0%
    :alt: Python installer window with arrows pointing to "Add Python to PATH" and "Install Now"

Make sure you check "Add Python to PATH", and go all the way through the
installer.

Log out and back in, or restart your computer. Whichever is easiest.

Open the start menu and type ``cmd``. Press the enter key.

In the terminal that comes up, check that Python is installed:

.. code-block:: console

    > python --version
    Python 3.10.1

.. note::

    Don't copy the ``>``. That's used to show that this is a command that goes
    in the console, and to let you see what the expected results are (shown on
    the next line without a ``>``)

Looks good? You can go ahead and install ESPHome:

.. code-block:: console

    > pip3 install wheel
    > pip3 install esphome

And you should be good to go! You can test that things are properly installed
with the following:

.. code-block:: console

    > esphome version
    Version: 2021.12.3

Mac
---

Your macOS probably already has Python 3 installed. 

.. code-block:: console

    % which python3
    /usr/bin/python3

However it does not work until Xcode is installed. Open App Store.app and 
download Xcode.app if not yet. Agreement to Xcode License is also required. 
Just open Xcode.app, and press the agree button in the initial dialog window.
Once the python3 is activated, confirm that it is at least version 3.7:

.. code-block:: console

    % python3 --version
    Python 3.8.9

Looks good? You can go ahead and install ESPHome:

.. code-block:: console

    % pip3 install --user esphome

You may get an error message saying that your pip is not the latest one. 
In that case, follow the instruction shown in the error message and type:

.. code-block:: console

    % pip3 install --upgrade pip

and try ``pip3 install --user esphome`` command again. ESPHome will be installed in 
~/Library/Python/3.8/bin directory (3.8 is the version number of Python 3 with macOS 12).
If you don't want to type the full path to ESPHome programs, you can run 
``echo 'export PATH=$PATH:$HOME/Library/Python/3.8/bin' >> $HOME/.zshrc``, 
then close and re-open your Terminal window.

At this point, you should be able confirm that ESPHome has been successfully installed:

.. code-block:: console

    % esphome version       
    Version: 2022.6.2

Linux
-----

Your distribution probably already has Python installed. Confirm that it is at
least version 3.7:

.. code-block:: console

    $ python3 --version
    Python 3.7.1

Looks good? You can go ahead and install ESPHome:

.. code-block:: bash

    pip3 install --user esphome

.. caution::

    Don't use ``sudo`` with pip. If you do, you'll run into trouble updating
    your OS down the road.

    For details, see `DontBreakDebian
    <https://wiki.debian.org/DontBreakDebian#A.27make_install.27_can_conflict_with_packages>`_.
    ``pip install`` is equivalent to ``make install`` in this context. The
    advice in the article applies to all Linux distributions, not just Debian.

At this point, you should be able confirm that ESPHome has been successfully installed:

.. code-block:: console

    $ esphome version
    Version: 2021.12.3

If you get an error like "Command not found", you need to add the binary to
your ``PATH`` using ``export PATH=$PATH:$HOME/.local/bin``.

To set this permanently, you can run ``echo 'export
PATH=$PATH:$HOME/.local/bin' >> $HOME/.bashrc``, then log out and back in.

See Also
--------

- :doc:`ESPHome index </index>`
- :doc:`getting_started_command_line`
- :ghedit:`Edit`
