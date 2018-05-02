=========================================================================
Provision CLOS fabric using Dell EMC Networking NAPALM APIs example
=========================================================================

This example describes how to use NAPALM to build a CLOS fabric with Dell EMC Networking OS10 switches.
The sample topology is a two-tier CLOS fabric with two spines and four leafs connected as mesh. EBGP is running between the two tiers.

All switches in spine have the same AS number, and each leaf switch has a unique AS number. All AS number used are private.
For application load-balancing purposes, the same prefix is advertised from multiple leaf switches and uses *BGP multipath relax* feature.


.. figure:: ./_static/topo.png
   :scale: 50 %
   :alt: map to buried treasure

STEP 1
~~~~~~

Download the CLOS fabric configuration by clicking the switch name below,

:download:`spine1 <config/spine1.cfg>` :download:`spine2 <config/spine2.cfg>` :download:`leaf1 <config/leaf1.cfg>` :download:`leaf2 <config/leaf2.cfg>` :download:`leaf3 <config/leaf3.cfg>` :download:`leaf4 <config/leaf4.cfg>`

Copy all the downloaded configuration file in the any directory here named ``/root/napalm/clos_configuration``

STEP 2
~~~~~~

Load/Merge configuration for all the switches in the fabric

Create a file called ``load_merge.py`` in a folder with the following content:

::

    from napalm_base import get_network_driver

    configs_dir = "/root/napalm/clos_configuration/" # add your configuration base directory path
    commit_config = False # If you are happy with the changes, mark this as True
    discard_config = True # Mark as True, To delete the uploaded configuration

    # Add your global switch credentials
    device_creds = {
        "username": "admin",
        "password": "admin",
        "optional_args": {
                "global_delay_factor": 3
        }
    }

    # Add your Switch specific details
    fabric_details = {
        "spine1": {
            "hostname" : "1.1.1.1",
            "config_file": "spine1.cfg"
        },
        "spine2": {
            "hostname": "1.1.1.2",
            "config_file": "spine2.cfg"
        },
        "leaf1": {
            "hostname": "1.1.1.3",
            "config_file": "leaf1.cfg"
        },
        "leaf2": {
            "hostname": "1.1.1.4",
            "config_file": "leaf2.cfg"
        },
        "leaf3": {
            "hostname": "1.1.1.5",
            "config_file": "leaf3.cfg"
        },
        "leaf4": {
            "hostname": "1.1.1.6",
            "config_file": "leaf4.cfg"
        }
    }

    driver = get_network_driver('dellos10')

    for key, value in fabric_details.iteritems():
        device_ip = value.get("hostname")
        config_file = configs_dir + value.get("config_file")

        device = driver(device_ip, **device_creds)
        device.open()
        print("{}: Started loading configuration ".format(key))
        device.load_merge_candidate(filename=config_file)
        print("Configuration difference to be applied on switch : {}".format(key))
        print(device.compare_config())

        if commit_config:
            device.commit_config()
            print("Configuration successfully loaded into switch: {}".format(key))

        if discard_config:
            device.discard_config()
            print("{}: Configuration discarded successfully".format(key))

        device.close()
