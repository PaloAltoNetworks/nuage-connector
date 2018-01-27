# pan-nuage

PAN-OS - Nuage integration code

##

Install requirements.txt

## Description

**pan-nuage.py** connects to the Nuage VSD server and retrieves information about VPorts and VMInterfaces in a given domain. This data is then pushed to PAN-OS devices using Dynamic Address Groups APIs.

### Interaction with Panorama

**pan-nuage.py** can automatically retrive the list of devices to use as push targets from Panorama. The devices should be registered on Panorama and tagged with a tag derived from from the Nuage domain to be monitored. 

Example: the tag associated to the Nuage domain 3b665b7f-9315-426a-bc9e-4e1d7e3f6124 is nuage-3b665b7f-9315.

The list of the tagged devices is checked on Panorama every 60 seconds.

### Supported tags

The following tags are supported:

* zone
* policygroup
* subnet

Example:

	admin@pv70> debug object registered-ip show tag-source ip 10.20.20.7 tag all 

	<response status="success"><result>
	registered IP                             Tags
	----------------------------------------  -----------------

	10.20.20.7 #
	                                         "zone-627659b8-4b5b-437e-bf39-33da138e5237"
	                                        [ SRC List: < XMLAPI > ]
	
	                                         "subnet-19bde716-f3e1-4b12-9ad5-b197fcc6554d"
	                                        [ SRC List: < XMLAPI > ]
	
	                                         "policygroup-c1621a11-a98e-4256-a70e-474360c97e3f"
	                                        [ SRC List: < XMLAPI > ]



## Usage

### Sample usage

	$ python2.7 pan-nuage.py --nuage-vsd 172.31.1.1:8443 --nuage-login csproot --nuage-password password --nuage-organization csp --nuage-domain 3b665b7f-9315-426a-bc9e-4e1d7e3f6124 --panorama 192.168.0.126 --pan-admin admin --pan-password admin
	
### Arguments

`--nuage-vsd <address:port>` address and port of Nuage VSD

`--nuage-login <username>` username for Nuage VSD

`--nuage-password <password>` password for Nuage VSD

`--nuage-organization <org>` organization for Nuage VSD

`--nuage-domain <domain id>` UUID of the Nuage domain to monitor

`--panorama <address>` address of Panorama

`--pan-admin <username>` username for Panorama

`--pan-password <password>` password for Panorama
