############
Installation
############

This information contains instructions to install `napalm_dellos10 <https://github.com/napalm-automation-community/napalm-dellos10>`_. Included is information on the setup environment for managing Dell EMC Networking OS10 switches using Python.

Install NAPALM
**************

Install the Dell Networking OS10 NAPALM driver:

::

   sudo apt-get install libffi-dev libssl-dev python-dev python-cffi libxslt1-dev python-pip
   sudo pip install --upgrade cffi
   sudo pip install https://github.com/napalm-automation-community/napalm-dellos10/archive/v1.0.5.zip 

Test your setup
***************

Open the Python interpreter terminal using "python":

::

    >>> from napalm_base import get_network_driver
    >>> d = get_network_driver('dellos10')
    >>> e = d('<HOSTNAME/IP_ADDRESS>', '<USERNAME>', '<PASSWORD>', optional_args={'global_delay_factor': 3})
    >>> e.open()
    >>> e.get_facts()
    >>> e.close()
