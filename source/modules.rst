#####################################
Dell EMC Networking OS10 NAPALM APIs
#####################################

NAPALM connect to the devices, to manipulate configurations or to retrieve data using the below APIs

More details about each API shall be `found here <https://napalm.readthedocs.io/en/latest/base.html>`_

Implemented APIs
----------------
- load_merge_candidate
- compare_config
- commit_config
- discard_config
- get_facts
- get_config
- ping
- get_snmp_information
- get_interfaces
- get_route_to
- get_interfaces_ip
- get_bgp_config
- get_bgp_neighbors_detail
- get_bgp_neighbors
- get_lldp_neighbors
- get_lldp_neighbors_detail
- get_lldp_neighbors_interface_detail
- install_switch_image
- upgrade_switch_image
- get_image_status

Missing APIs
------------

- rollback is not supported
- load_replace_candidate not supported