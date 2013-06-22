xen-scripts
===========
A sweet of scripts for automation and daily administration of xen dom0s.

vmbackup
--------

Backups up LVM based domus using snapshots. A broad shell script for opensource xen backup or virtual machine (vm) backup.

### Features 

 - Support for libxl configuration
 - Backup one domu or all
 - Backup to a mounted external drive or CISF etc.
 - Backup xl configuration as well
 - Inline and live progress
 - Computes overall backup time
 - Interactive and non-interactive mode
 - Support for plain text output, especially for mailx and cronjobs
 - Builtin checks and error handling for LVM snapshots
 - Ability to compress using lzop and save out zero blocks

### Configuraitons

	BACKUP_DIR=/path/to/backup
	PROCESS_DIR=/path/to/local
	XL_CONF_DIR=/home/cfgs
	SNAPSHOT_PREFIX=snap
	SNAPSHOT_SIZE=100G

`PROCESS_DIR` sets the local path where the domu images are stored temporarily.
`XL_CONF_DIR` sets the configuration path where xl domu configuration files exist.
`SNAPSHOT_SIZE` should be set to a maximum 30-40% of the largest domu LVM. It is important that you set it up because auto-expansion of LVM is quite buggy by design if you are aiming to do that in /etc/lvm/lvm.conf. See snapshot_autoextend_threshold and snapshot_autoextend_percent in man(5) lvm.conf for details. Another reason for setting this to a high value is that if the snapshot size exceeds the size of image during backup, you might end up with a dirty backup itself!

### Command-line Options

	vmbackup one [domu_name]

will backup one domu vm interactively, name as shown in xl list

	vmbackup -c one [domu_name]

will do the same (run through a cronjob)

	vmbackup -c all 

will backup all domus (run through a cronjob)

### Sample Output

![Image](./vmbackup.png?raw=true)



listvncs
--------
Lists domus and their listening vnc ports

### Sample Output

	domUs                sockets             
	-----                -------             
	mushy                172.16.1.3:5909
	troublesome          172.16.1.3:5911
	snotty				 172.16.1.3:5903
