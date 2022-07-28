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

There are no tested installation instructions for Mac. ESPHome does support
Mac & will run with no problem.

Contributions are welcome!

The process will likely be similar to Windows. You can install Python from the
official site, and then install ESPHome with ``pip3 install esphome``.  You can
then test that things are properly installed with the following:

.. code-block:: console

    $ esphome version
    Version: 2021.12.3

-----------
memo


% which python
python not found

% which python3
/usr/bin/python3

% python3 --version
xcode-select: note: no developer tools were found at '/Applications/Xcode.app', requesting install. Choose an option in the dialog to download the command line developer tools.

% python3 --version
xcode-select: note: no developer tools were found at '/Applications/Xcode.app', requesting install. Choose an option in the dialog to download the command line developer tools.

% python3 --version


You have not agreed to the Xcode license agreements. You must agree to both license agreements below in order to use Xcode.

Press the 'return' key to view the license agreements at '/Applications/Xcode.app/Contents/Resources/English.lproj/License.rtf'


Agreeing to the Xcode/iOS license requires admin privileges, please run “sudo xcodebuild -license” and then retry this command.




You have not agreed to the Xcode license agreements. You must agree to both license agreements below in order to use Xcode.

Press the 'return' key to view the license agreements at '/Applications/Xcode.app/Contents/Resources/English.lproj/License.rtf'

% python3 --version
2022-07-28 23:32:45.901 xcodebuild[2064:102337] Requested but did not find extension point with identifier Xcode.IDEKit.ExtensionSentinelHostApplications for extension Xcode.DebuggerFoundation.AppExtensionHosts.watchOS of plug-in com.apple.dt.IDEWatchSupportCore
2022-07-28 23:32:45.901 xcodebuild[2064:102337] Requested but did not find extension point with identifier Xcode.IDEKit.ExtensionPointIdentifierToBundleIdentifier for extension Xcode.DebuggerFoundation.AppExtensionToBundleIdentifierMap.watchOS of plug-in com.apple.dt.IDEWatchSupportCore
Python 3.8.9

% python3 --version
Python 3.8.9
% pip3 --version
pip 20.2.3 from /Applications/Xcode.app/Contents/Developer/Library/Frameworks/Python3.framework/Versions/3.8/lib/python3.8/site-packages/pip (python 3.8)

pip3 install -user esphome

Error がでるので、pipをアップグレードする　　

% pip3 install --upgrade pip

export PATH=$PATH:$HOME/Library/Python/3.8/bin/

% echo 'export PATH=$PATH:$HOME/Library/Python/3.8/bin/' >> $HOME/.zshrc








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
