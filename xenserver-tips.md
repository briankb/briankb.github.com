XenServer 6.0 Tips, Tricks, and things I've learned so far
----------

the default ISO folder is located  at /opt/xensource/packages/iso

* **COPY** all of your ISO's for VM's there before attempting to install from a network share on a DSL or Cable speed connection.
An iSCSI that's local to the datacenter is ok but anything else just isn't fast enough.

* you must create storage resources from RAID arrays correctly in order for them to work. This wasn't my mistake but something I learned from Tech Support.
