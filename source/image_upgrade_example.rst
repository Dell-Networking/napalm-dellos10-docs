============================================================================
Use NAPALM to install or upgrade devices running Dell EMC Networking OS10
============================================================================

This example explains how to use NAPALM to install or upgrade the software image on a device running Dell EMC Networking OS10.


STEP 1
~~~~~~
Make sure switches are accessible through NAPALM

Open the Python interpreter terminal using "python" and type the below line by line,

::

    >>> from napalm_base import get_network_driver
    >>> d = get_network_driver('dellos10')
    >>> e = d('<HOSTNAME/IP_ADDRESS>', '<USERNAME>', '<PASSWORD>', optional_args={'global_delay_factor': 3})
    >>> e.open()
    >>> e.get_facts()
    >>> e.close()

STEP 2
~~~~~~~

Upload the image you need to install to any of the TFTP/FTP/SCP/SFTP/HTTP server

STEP 3
~~~~~~~
Install or upgrade the image on the switch as below,

Example image file path:

SCP server details are below,
``Server IP``: 1.1.1.1
``credentials``: username: my_username, password: my_password
``image file path``: /root/PKGS_OS10-Enterprise-10.4.0E.R2.30-installer-x86_64.bin

then our ``image_file_url`` should look as below

``image_file_url="scp://my_username:my_password@1.1.1.1/root/PKGS_OS10-Enterprise-10.4.0E.R2.30-installer-x86_64.bin"``

To install the switch image run the below python file:

Create a file called ``image_upgrade.py`` in a folder with the following content:

::

    from napalm_base import get_network_driver

    # Add your global switch credentials
    device_creds = {
        "username": "admin",
        "password": "admin",
        "optional_args": {
                "global_delay_factor": 3
        }
    }

    image_file_url="scp://my_username:my_password@1.1.1.1/root/PKGS_OS10-Enterprise-10.4.0E.R2.30-installer-x86_64.bin"

    driver = get_network_driver('dellos10')


    device = driver("1.1.1.1", **device_creds)
    device.open()
    print("Switch image install started...")
    device.install_switch_image(image_file_url=image_file_url)
    # get the switch status using below
    device.get_image_status()

    device.close()


.. note::

   ``image_file_url`` format for TFTP/FTP/SCP/SFTP/HTTP server are below

            - ``ftp``:    Install from remote FTP server (ftp://userid:passwd@hostip/filepath)
            - ``http``:   Install from remote HTTP (http://hostip/filepath)
            - ``image``:  Install from image directory (image://filepath)
            - ``scp``:    Install from remote SCP server (scp://userid:passwd@hostip/filepath)
            - ``sftp``:   Install from remote SFTP server (sftp://userid:passwd@hostip/filepath)
            - ``tftp``:   Install from remote TFTP server (tftp://hostip/filepath)
            - ``usb``:    Install from USB directory (usb://filepath)

