----------------------------------------------------------------------------------------------------------------------------------------
 armour.tcl v3.4.2 - 2020.01.15
----------------------------------------------------------------------------------------------------------------------------------------

 ![Armour](./armour.png)

 Anti abuse script for eggdrop bots on the Undernet IRC Network

----------------------------------------------------------------------------------------------------------------------------------------
 NOTES FOR ARMOUR UPDATES
----------------------------------------------------------------------------------------------------------------------------------------

 This file should be monitored for feature enhancements that require consideration.
 Specifically, look for new config variables that have eventuated through new features.  Find these variables
 from the armour.conf.sample file provided and paste into your own *.conf file with appropriate values.

----------------------------------------------------------------------------------------------------------------------------------------

***2019.01.15	v3.4.2***

	+ New release Armour v3.4.2
	
	+ Enhancement:	adduser no longer requires temporary password
	+ Enhancement:  tell plugin context fixes and improvements
	+ Enhancement:	alert users upon autologin when no password is set
	
		- Config var:	arm(cfg.alert.nopass): enabled or disabled

-----------------------------------------------------------------------------------

***2019.12.21	v3.4.1***

	+ Fixed bug:	autologout when using sqlite, not working 
	+ Fixed bug:	autologin not working first time for a new user
	+ Fixed bug:	newpass not working
	+ Enhancement:	changed userline separator from : to | to support IPv6 hosts
	+ Enhancement:  cmdlog now logs to report channel

----------------------------------------------------------------------------------------------------------------------------------------

***2019.03.17	v3.4.0***

	+ New release Armour v3.4.0

	+ Fixed bug:	issues with secure mode preventing stable operation

	+ Enhancement:	allow 'country' blacklist entries to be ignored when user has resolved ident

		- Config var:	arm(cfg.country.ident): enabled or disabled

----------------------------------------------------------------------------------------------------------------------------------------

***2019.01.21	v3.3.3.0***

	+ Fixed bug:	scans halting from clients with nicks or realnames using special chars

----------------------------------------------------------------------------------------------------------------------------------------

***2014.10.06	v3.3.2.0***

	+ Fixed bugs:	various small fixes

----------------------------------------------------------------------------------------------------------------------------------------

***2014.09.29	v3.3.1.0***

	+ Enhancement:	support for 'email' and 'languages' user attributes

----------------------------------------------------------------------------------------------------------------------------------------

***2014.09.28	v3.3.0.0***

	+ Enhancement:	support optional sqlite3 databases

		- Config var:	arm(method):	'file' or 'sqlite'

----------------------------------------------------------------------------------------------------------------------------------------

***2013.02.15	v3.2.2.0***

	+ Fixed bug:	invalid references to paranoid(scanlist) var

	+ Fixed bug:	invalid references to scanlist var

	+ Fixed bug:	arm:db:write was duplicating timers

	+ Enhancement:	cmd 'save' now saves userdb and white & black lists, providing stats on both

	+ Enhancement:	cmd 'load' now loads userdb and white & black lists, providing stats on both

	+ Enhancement:	allow channel name visibility in channel blacklist kick reason to be configurable

		- Config var:	arm(cfg.bchan.reason):	enabled or disabled

----------------------------------------------------------------------------------------------------------------------------------------

***2011.12.26	v3.2.1.2***

	+ Fixed bug:	mode 'secure' was causing infinite scan loops

----------------------------------------------------------------------------------------------------------------------------------------

***2011.12.06	v3.2.1.1***

	+ Enhancement:	allow user specific automode actions (none, voice, op)

		- Modified commands: adduser, moduser, whois

----------------------------------------------------------------------------------------------------------------------------------------

***2011.11.22	v3.2.1.0***

	+ Added cmd:	moduser:	modifies an existing users username, level, xuser or password

	+ Added cmd:	userlist:	views entire userlist

	+ Added cmd:	die:		kills the bot entirely

	+ Added cmd:	say:		has the bot send a message to a channel, all channels or a given nickname.  
					optionally can be an action.

	+ Enhancement:	cmd 'whois' can now lookup via nickname with = prefix (a la Undernet's X / 
			gnuworld mod.cservice)
			ie. 'whois =nick' will check if 'nick' is logged in and if so, execure 'whois' on that username

	+ Fixed bug:	ipv6 IP space was breaking scan results

	+ Fixed bug:	nicks with special chars breaking scanner

	+ Fixed bug:	no whitelist action been taken for channel entries

	+ Fixed bug:	autologout anomoly

	+ Fixed bug:	nick change anomoly

	+ Enhancement:	allow nickname and global command char prefixes

		- Config var:	arm(cfg.char.nick):	whether to allow nickname as command prefix
		- Config var:	arm(cfg.char.tab):	whether nick completion is required (with tailing ':' char on 
							nickname)
		- Config var:	arm(cfg.char.glob):	whether global command prefix char '*' can be used (to say, 
							control all bots in a channel)

	+ Enhancement:	control whether or not command shortcuts are enabled

		- Config var:	arm(cfg.cmd.short):	enabled or disabled

----------------------------------------------------------------------------------------------------------------------------------------

***2011.03.17	v3.2.0.6***

	+ Added plugin:		support for libdronebl (add, remove & view dronebl submissions)
				note: you need your own RPC2 key from www.dronebl.org for this and are responsible for 
				your own submissions.

		- Config var:	arm(cfg.dronebl.lvl):	level required for DroneBL submission
		- Config var:	arm(cfg.donrebl.type):	default DroneBL submit type

	+ Enhancement:		introduced additional metrics to help determine which clients to voice when in mode 
				'secure':
					- clones (IP or host)
					- signon age
					- trakka plugin score (optional)
				bot will send opnotice to channel when cannot make a safe choice to voice client.

		- Config var:	arm(cfg.paranoid.clone):	number of clones to mark for manual review (no 
								autovoice) 
		- Config var:	arm(cfg.paranoid.signon):	server connection time must be older than N seconds for 
								autovoice
		- Config var:	arm(cfg.paranoid.trakka):	minimum trakka score (if plugin loaded) to gain 
								autovoice

----------------------------------------------------------------------------------------------------------------------------------------

***2011.02.19	v3.2.0.4***

	+ Added feature:	ability to specify which G-Line patterns will /not/ add blacklist entry
		- Config var:	arm(cfg.gline.nomask):	wildcard pattern for G-Lines not to add				

	+ Fixed bug:		cmd 'help' was only working for level 500 users

----------------------------------------------------------------------------------------------------------------------------------------

***2011.01.30	v3.2.0.3***

	+ Fixed bug:		- stats command not always working

	+ Added feature:	- commands 'add' 'rem' and 'view' now support comma delimited values 
					ie. b add black user1,user2,user3,user4 ban abuse is not tolerated!

----------------------------------------------------------------------------------------------------------------------------------------

***2011.01.15	v3.2.0.1***

	+ Introduce Tcl 8.6 coroutines for asynchronous:
		- dnsbl lookups
		- port scans
		- geo lookups
		- asn lookups

		(big performance gains!)

	+ Added cmd:	restart:	saves db & restarts bot

	+ Added cmd:	status:		retrieves current bot status, uptime, traffic usage etc

	+ Added cmd:	jump:		jumps bot server

	+ Added cmd:	rehash:		saves db & rehashes bot

----------------------------------------------------------------------------------------------------------------------------------------

***2010.09.18	v3.1.2.1***

	+ Tidied idents from double space -> tabs (makes for cleaner code)

	+ Added md5 option	allows for different md5 binaries
		- Config var:	arm(cfg.md5):	either 'md5' (common bsd) or 'md5sum' (linux)

	+ Added feature:	tracking of recently joined hosts, for fast blacklist additions
		- Config var:	arm(cfg.lasthosts):	how many recent hosts to hold in memory

	+ Added feature:	'last' method when adding whitelist & blacklists
				- last <N>	will add the last N entries to the blacklist/whitelist either type host 
						or user (if umode +x)

		- Config var:	arm(cfg.lasthosts):	how many recent hosts to track

	+ Added feature:	- /silence protection for bot
		- Config var:	arm(cfg.silence):	list of silence masks (including exclusions) to set on server 
							connection

	+ Added feature:	- add automatic bans on blacklist entry (host/user)
		- Config var:	arm(cfg.ban.auto):	boolean -- add automatic bans on blacklist?

	+ Added feature:	- add automatic unbans on blacklist removal (host/user)

	+ Added enhancement:	- prevent a blacklist entry being added for a value that is whitelisted
				- prevent a whitelist entry being added for a value that is blacklisted

	+ Added enhancement:	- configurable default exempt time via 'exempt' command:
		-  Config var:	arm(cfg.exempt.time):	default time in minutes a nick is exempt from scans for 
							upon /join

				- added extra arg [mins] to exempt command to override the above default.
				usage: exempt <nick> [mins]

	+ Added enhancement:	- added Armour plugin support
				- script:	trakka		(tracks channel regulars and notified channel when 
								unknown clients join)
				- script:	smsbot		(basic sms gateway with acl supported phonebook)
				- script:	tell		(interface for bot to tell users certain things based on 
								time, timers or activity)

	+ Added enhancement:	new modular help topics using individual help files

	+ Added enhancement:	complete rewrite of command binds
				- every command can now be enabled/disabled invidually with a unique level for public, 
				privmsg and dcc binds if desired
		- Config vars removed:
				- arm(cfg.cmd.pub)
				- arm(cfg.cmd.msg)
				- arm(cfg.cmd.dcc)
		- Config section added:
				- command levels:	use 'set addcmd(...)' to toggle commands and acl's

	+ Added enhancement:	- added optional ?chan? arg to commands: op, deop, kick, voice, devoice

	+ Added enhancement:	- new command:	invite:	invite ?chan? [nick1] [nick2] [nick3] [nick4] [nick5] [nick6]....

	+ Fixed bug:		- autologin was not always starting on server jump

	+ Added enhancement:	- included list ID to DNSBL blacklist kick reasons

	+ Tidied output:	- removed 'NULL' from DNSBL blacklist kick reasons if no info returned

	+ Fixed bug:		- 'stats' command not returning accurate information. stats not being saved to db 
				file correctly.

	+ Fixed bug:		- new ACL system was only allowing level 500 users to use commands in privmsg.

----------------------------------------------------------------------------------------------------------------------------------------

***2010.09.18	v3.1.2***

	+ Added feature:	statistical hit counts for blacklist & whitlist entries

	+ Added script:		upgrade.sh
					- upgrade existing DB files to allow new statistical hit field.

					NOTE: 	- This *MUST* be done manually before loading new code: 
						usage: ./upgrade.sh <armour-dbfile>
						- DB file is set in config var 'arm(cfg.db.file)' 
						userfile requires no upgrade

	+ Added feature:	integration proc redirection for external scripts
		- Config var:	arm(cfg.integrate.procs):	List of procs to send 'nick uhost hand chan' to after 
								sucessful whitelist, or passing blacklists

	+ Added enhancement:	now kicking any clients where host is matched during floodnet detection (even if that 
				client wasn't a match)

----------------------------------------------------------------------------------------------------------------------------------------

***2010.09.08	v3.1.1***

	+ Created UPDATING.txt file to assist in the knowledge of new features and config variables

	+ Added feature:	automatic blacklist entry on G-Line
		- Config vars:	arm(cfg.gline.auto):	Add automatic blacklist entry on GLine?
				arm(cfg.gline.mask):	Optional G-Line reason pattern for above to apply

	+ Added feature:	open port number threshold -- required N number of open ports to be detected before 
				kickban action
		- Config var:	arm(cfg.portscan.min):	minimum open ports before kickban

----------------------------------------------------------------------------------------------------------------------------------------

***2010.09.07	RECORD BEGINS***
