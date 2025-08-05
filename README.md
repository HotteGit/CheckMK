
vi /usr/lib/check_mk_agent/plugins/http_check_remote

mkdir -p ~/local/lib/python3/cmk_addons/plugins/network_checks_custom/agent_based
vi ~/local/lib/python3/cmk_addons/plugins/network_checks_custom/agent_based/http_check_remote.py

mkdir -p  ~/local/lib/python3/cmk_addons/plugins/network_checks_custom/rulesets
vi  ~/local/lib/python3/cmk_addons/plugins/network_checks_custom/rulesets/ruleset_http_check_remote.py


cmk --detect-plugins=http_check_remote -v localhost

	+ FETCHING DATA
	Get piggybacked data
	[['url=https://chat.stang66.de:443', 'code=200', 'expected_code=200']]
	Parameters({})
	HTTP Check (remote) https://chat.stang66.de:443 HTTP code 200 as expected for https://chat.stang66.de:443
	[agent] Success, [piggyback] Success (but no data found for this host), execution time 0.8 sec | execution_time=0.840 user_time=0.020 system_time=0.010 children_user_time=0.000 children_system_time=0.000 cmk_time_agent=0.810


OMD[monitoring]:~$ mkp template http_check_remote
	Created '/omd/sites/monitoring/tmp/check_mk/http_check_remote.manifest.temp'.
	You may now edit it.
	Create the package using `mkp package /omd/sites/monitoring/tmp/check_mk/http_check_remote.manifest.temp`.
	OMD[monitoring]:~$ vi /omd/sites/monitoring/tmp/check_mk/http_check_remote.manifest.temp


OMD[monitoring]:~$ mkp package /omd/sites/monitoring/tmp/check_mk/http_check_remote.manifest.temp


OMD[monitoring]:~$ mkp add ./var/check_mk/packages_local/http_check_remote-1.0.0.mkp
	Package http_check_remote 1.0.0 exists on the site!

OMD[monitoring]:~$ mkp enable http_check_remote

OMD[monitoring]:~$ mkp show-all
	Local extension packages
	========================

	Name:                          http_check_remote
	Version:                       1.0.0
	Packaged on Checkmk Version:   cmk-mkp-tool 1.0.0
	Required Checkmk Version:      2.4.0p7
	Valid until Checkmk version:   No version limitation
	Title:                         HTTP(S)eck (remote)
	Author:                        Roberte
	Download-URL:                  https://example.com/http_check_remote/
	Files:
	  Agents
		plugins/http_check.py
	  Additional Checkmk plug-ins by third parties
		network_checks_custom/agent_based/http_check_remote.py
		network_checks_custom/rulesets/ruleset_http_check_remote.py
	Description:
	  Check for HTTP port from remote machine, when direct check from CheckMK Server is not possible.

	Shipped extension packages
	==========================

