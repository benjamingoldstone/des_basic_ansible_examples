# Gathering Info From Devices

## Intro

This part of the project focuses on gathering info from devices running Dell Enterprise SONiC. You can use these examples to gather basic info, validate configurations and more. 
 
Note that for the playbook 'gather_facts.yaml', the variable 'network_subset_to_gather_(target)' is used to specify what info to pull from the device. Per the documentation possible values for this argument include all, min, hardware, config, legacy, and interfaces. 

Similarly, 'network_resources_to_gather_(target)' specifies sections of the running configuration to retrieve. Valid options are shown below. Note that you can specify a list of values to include a larger subset. Values can also be used with an initial '!' to specify that a specific subset should not be collected.

  * all
  * vlans
  * interfaces
  * l2_interfaces
  * l3_interfaces
  * lag_interfaces
  * bgp
  * bgp_af
  * bgp_neighbors
  * bgp_neighbors_af
  * bgp_as_paths
  * bgp_communities
  * bgp_ext_communities
  * mclag
  * prefix_lists
  * vlan_mapping
  * vrfs
  * vxlans
  * users
  * system
  * port_breakout
  * aaa
  * tacacs_server
  * radius_server
  * static_routes
  * ntp
  * logging
  * ip_neighbor
  * port_group
  * dhcp_relay
  * acl_interfaces
  * l2_acls
  * l3_acls
  * lldp_global
  * mac
  * bfd
  * copp
  * route_maps


## Requirements

Note that this project requires the following:

  * python 3.8.5 or newer
  * pip3 20.2.4 or newer

It is recommended that you create a python virtual environment with the command:

`python -m venv venv`

You'll then activate the virtual environment with:

`source ./venv/bin/activate`

Be sure to install the most current version of the Dell Enterprise SONiC Ansible Collection from Ansible Galaxy with:

`ansible-galaxy collection install dellemc.enterprise_sonic`

From there you should be able to modify the inventory/hosts.yaml file with your appropriate IP addresses and then run the example playbook with:

`ansible-playbook -i inventory/hosts.yaml playbook_gather_facts.yaml`


## Tips and Tricks

### x509 certificate error

If you recieve an x509 certificate error you may need to ensure you're running a recent version of pyopenssl with:

`pip install pyopenssl --upgrade`

### Make JSON files more readable

Note that you can easily make JSON files output by the gather facts playbook more readable by running them through jq (if installed obviously):

`cat ./output/spine1_output.json | jq '.' > ./output/modified_spine1_output.json`

