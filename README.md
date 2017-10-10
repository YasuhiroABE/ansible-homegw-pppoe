YasuhiroABE.homegw-pppoe
=========

This role sets up pppoe for the home router.
It expects the home router connected with pppoe to ISP like FLET's fiber-optic internet service.

Requirements
------------

This role is tested on the following platforms.

### Ansible
- Version 2.4

### Distributions
- Ubuntu 16.04
- Debian 9


Role Variables
--------------

### Default

	homegw_pppoe_pppinfo_list: {}
	* format: dsl-provider: { userid: xxxx@example.org, password: xxxxxxxx, device: eth0 }

	homegw_pppoe_papsecrets_permission:
	  owner: root
	  group: root
	  mode: '0400'
	* Set the permission of the /etc/ppp/pap-secret file
	  
	homegw_pppoe_peersfile_permission:
	  owner: root
	  group: dip
	  mode: '0640'
	* Set the permission of /etc/ppp/peers/* files.

	homegw_pppoe_ipv6_enable: False
	* If True, the pppoe-ipv6-up script will be placed.

	homegw_pppoe_ipv6_eth_device: 'ppp2'
	* If homegw_pppoe_ipv6_enable is True, the ipv6 ppp device name must be placed.
	
    homegw_pppoe_internal_eth_device: 'eth1'
	* If homegw_pppoe_ipv6_enable is True, the internal eth device name must be placed to allocate the site level ipv6 prefix.

Dependencies
------------

N/A

Example Playbook
----------------

    - hosts: all
	  vars:
	    homegw_pppoe_pppinfo_list:
		  default: { userid: xxx@example.org, password: xxxxxx, device: ppp1 }
		  ipv6: { userid: yyy@example.org, password: xxxxxx, device: ppp2 }
		homegw_pppoe_ipv6_enable: True
		homegw_pppoe_ipv6_eth_device: ppp2
		homegw_pppoe_internal_eth_device: 'eth1'
      roles:
        - YasuhiroABE.homegw-pppoe

License
-------

Apache License 2.0

Author Information
------------------

[Yasuhiro ABE](http://www.yasundial.org/foaf.xml)

