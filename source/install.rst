############
Installation
############

This section contains instructions to install `napalm_dellos10 <https://github.com/napalm-automation-community/napalm-dellos10>`_.

we shall cover the setup environment for managing Dell Networking OS10 switches

Install instruction given below is for Linux Debian.

Install Napalm
--------------

Install Dell Networking OS10 NAPALM driver,

::

   sudo apt-get install libffi-dev libssl-dev python-dev python-cffi libxslt1-dev python-pip
   sudo pip install --upgrade cffi
   sudo pip install napalm-dellos10

Test your setup
---------------

Open the Python interpreter terminal using "python" and type the below,

::

    >>> from napalm_base import get_network_driver
    >>> d = get_network_driver('dellos10')
    >>> e = d('<HOSTNAME/IP_ADDRESS>', '<USERNAME>', '<PASSWORD>', optional_args={'global_delay_factor': 3})
    >>> e.open()
    >>> e.get_facts()
    >>> e.close()

