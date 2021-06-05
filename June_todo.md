# homelab
## TODO June 2021
- [ ] add pfsense router and move dream machine pro to inside network
- [x] fix plex
	- [x] restored from backup
- [x] fix pi hole
	- [x] firewall block on UDM 	
- [ ] restore usenet services
- [x] add remote management access
	- [x] via unraid.net
	- [x] add unraid.net DNS rebinding
	- [x] adjust firewall settings on UDM	
	- [ ] verify flash remote backups
	- [ ] confirm 
- [x] add unassigned plex drive
	- [x] preclear drive
	- [x] create pool
		- [x] add drive to pool
		- [x] create share
	- [x] copy plex drive meta to share
- [x] change minimum cache level to 1% empty
- [ ] fix SSL renewal situation with homelab, priority nextcloud
- [ ] fix duplicati
- [ ] fix perfex crm -bravo
- [ ] fix NZBget
- [ ] unzip tar files via terminal , tar -xvf
- [x] copy over /appdata files
- [x] add backup cache drive
- [ ] update CRM 1
- [ ] update CRM 2
- [x] stop server, add cache drive, add fans
- [x] ordered 1TB SSD
- [x] verify ombi.
- [x] verify app.plex.tv
- [ ] stop array
	- [ ] change drive name to identify class (nvme/ssd)
	- [ ] rename plex-cache-old to backup-appdata
	- [ ] create share on backup-appdata 
---
# 2021 Week of June 1
# issues with cache drive (docker images/appdata)
- loop2 errors in `sys log` -> diagnose as cache related issue
    - moved `appdata` to secondary drive
        > install unassigned devices app, mount SSD
		- on Unraid 6.9, created cache pool
        > stop plex docker
	> Use Krusader or `cp` to move plex app data folder (with metadata) to SSD
        > Edit plex docker and point `appdata` to new location
        > Make sure SSD is formated to not `ntfs` (`xfs` or something should work fine).
        
     - backed up appdata -> `/mnt/user/backups/appdata-backup` -> BACKUP BRAVO
     - formatted `/mnt/cache` as `xfs`
     - restored `appdata` using UnRaid CA Backup/Restore -> BACKUP ALPHA (weekly job)
     	- ends during restoration at similar points for both backups, see [1] below.
     - manual unpacking tar.gz backup via SSH 
	    - `gzip: CA_backup.tar.gz: unexpected end of file`
    		- `tar -tf` 	errors out
	    	- `tar -tif`	errors out
    		- `tar -xf`	errors out
	    	- `gunzip`	errors out
	    - `gzip stdin: unexpected end of file
	       tar: Error is not recoverable: exiting now`
	    - [1] both backups (ALPHA & BRAVO) fail, always on .bif file 
	    - `/Plex-Media-Server/Library/Application Support/Plex Media Server/Media/localhost/0/{hash}ca.bundle/Contents/Indexes/index-sd.bif`
	    

