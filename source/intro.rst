############
Introduction
############

This documentation explains the usage of NAPALM for deploying the configuration into Dell networking OS10 switches

NAPALM
******

NAPALM (Network Automation and Programmability Abstraction Layer with Multivendor support) is a Python library that
implements a set of functions to interact with different network device Operating Systems using a unified API.

NAPALM tries to provide a common interface and mechanisms to push configuration and retrieve state data from network devices.
This method is very useful in combination with tools like Ansible/Saltstack, which in turn allows you to manage a set of
devices independent of their network OS.

See `More information about NAPALM <https://napalm.readthedocs.io/en/latest/tutorials/index.html>`_.

Dell EMC Networking NAPALM integration
**************************************

Dell EMC Networking OS10 switches can be managed and automated using NAPALM unified API to manipulate configurations or
to retrieve data.
