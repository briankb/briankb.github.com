XenServer 6.0 Tips, Tricks, and things I've learned so far
----------

the default ISO folder is located  at /opt/xensource/packages/iso

* **COPY** all of your ISO's for VM's there before attempting to install from a network share on a DSL or Cable speed connection.
An iSCSI that's local to the datacenter is ok but anything else just isn't fast enough.

* you must create storage resources from RAID arrays correctly in order for them to work. This wasn't my mistake but something I learned from Tech Support.

* list of mirrored Linux distros on SoftLayer's Network
  * http://mirrors.service.softlayer.com/

* adding ip's
  * For your networking question you just have to assign the "Virtual Interfaces" in xencenter, so for example, eth0 and eth1 for private and public network.  Then all you should need to do is bind the IP in the OS, and XenServer will detect the IP you are using and show it in XenCenter for Networking on that VM