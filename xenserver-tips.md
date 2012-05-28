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

* create ISO directory
  * > "xe sr-create name-label="MyISORepository" type=iso device-config:location=/var/opt/xen/iso_import/ device-config:legacy_mode=true content-type=iso"
  * > "The easiest way is to use "xe pbd-unplug" and then "xe pbd-plug". This will refresh the SR by forcing it to be reread into the XAPI database. To get the universal unique Id of the PBD, please use a command similiar to the following:
xe pbd-list sr-uuid= <UUID of the SR
Then proceed to use:
xe pbd-unplug uuid=< UUID of the PBD
xe pbd-plug uuid=< UUID of the PBD>"

### Creating a Larger ISO folder from root XenServer drive
* Step by Step
  * [root@svr]# vgdisplay >> vgd.txt
    * doing this because the vgname in XenServer is too long to type, grab the full name from the txt file. I'm using PowerShell and cygwin SSH so this was the only way I could find to copy/paste 
  * now follow the steps in the Citrix support article CTX116350, I created a 30gb partition instead of a 12gb
* Resources
  * [How to Add Space to Your XenServer Host ISO Directory](http://support.citrix.com/article/CTX116350)
  * [XenServer: Creating an ISO Partition on DOM0](http://wagthereal.com/2011/11/18/xenserver-creating-an-iso-partition-on-dom0/)
  * [SoftLayer Mirrors](http://mirrors.service.softlayer.com)

### Using wget to Download CentOS files directly from SoftLayer mirror to XenServer ISO folder
* wget --limit-rate=100M (insert URL for ISO here) avg rate was 300kbps and it moved two ISO about 4gb in 125 seconds
* Resource for 15 wget examples http://www.thegeekstuff.com/2009/09/the-ultimate-wget-download-guide-with-15-awesome-examples/

### LVM Tips and Resources
* lvm - 
* pvs, pvdisplay, and pvscan - displays all physical partitions
* vgdisplay - show volume groups
* [RedHat LVM Docs](http://docs.redhat.com/docs/en-US/Red_Hat_Enterprise_Linux/5/pdf/Logical_Volume_Manager_Administration/Red_Hat_Enterprise_Linux-5-Logical_Volume_Manager_Administration-en-US.pdf)

### General Linux Tips & Commands
* scp - secure file transfer between servers
* wget - command line file downloader and spider
* ln -s - create a symbolic link between source and link-name
* 
* [The Ultimate Wget Download Guide With 15 Awesome Examples](http://www.thegeekstuff.com/2009/09/the-ultimate-wget-download-guide-with-15-awesome-examples/)
* [How to list or find the largest files and directories-folders, Free disk space](http://www.go2linux.org/linux/2010/11/how-list-or-find-largest-files-and-directories-folders-linux-free-disk-space-850)

### scp and WinSCP are your new best friend!
* waisted 30m trying to resolve a permissions is to transfer a ISO from one server to the other then I found an article describing scp to do it...
* scp my-local-file.iso root@10.10.10.1:/usr/jj/my-local-file.iso
* didn't even setup a SSH key just used root and it prompted for password. DONE!