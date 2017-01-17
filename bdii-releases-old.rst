Update: Update 8 - 29.04.2014 Name & Version 	Platform 	Release notes 	Installation & configuration
glite-info-provider-service 1.13.3-1 	EMI 3 SL5, EMI 3 SL6 	

BUG #102207: The service provider configuration for the RTEPublisher takes its version number from the lcg-info-dynamic-software RPM. As of EMI 3 the software provider is in glite-ce-cream-utils. This version of the service provider uses the right RPM.
	

None. Note that the rpms can be found for the time being in the Linuxsoft repositoy but they will be also available in the EMI repositories in the next update cycle scheduled for the beginning of May 2014.
Update: Update 7 - 10.04.2014 Name & Version 	Platform 	Release notes 	Installation & configuration
glue-validator 2.0.22 	EMI 3 SL5, EMI 3 SL6 	

BUG #48: bug in the test that validates GLUE2ComputingShareTotalJobs as reported by ARC. The test was wrongly counting twice a subset of jobs already included in other job attributes.
	

None. Note that the rpms can be found for the time being in the Linuxsoft repositoy but they will be also available in the EMI repositories in the next update cycle scheduled for the beginning of May 2014.
Update: 6 - 06.03.2014 Name & Version 	Platform 	Release notes 	Installation & configuration
glue-validator 2.0.21 	EMI 3 SL5, EMI 3 SL6 	

New version of glue-validator containing a set of updates and new features:

BUG #45: A workaround has been applied until the fix for ARC bug (see GGUS 99157 (link is external)) is widely deployed. Validity values of 60s won't raise the obsolete entry error (E002) until further notice.

BUG #44: New service and interface types for DPM have been added.

BUG #27: New service and interface types for QCG have been added

BUG #33: A new value 'lhcb' value has been added to the --testsuite option to run specific tests interesting for LHCb.

BUG #25: A margin of +-1 has been added to the total storage capacity attributes.

 

 

 
	

None
 
Update: 5 - 02.12.2013 Name & Version 	Platform 	Release notes 	Installation & configuration
emi-bdii-top 1.0.2-2 	EMI 3 SL5, EMI 3 SL6, EMI 2 SL5, EMI 2 SL6 	

BUG #8: This release decommissions the FCR (Freedom of Choice of Resources) mechanism that is no longer needed in the top BDII. The dependencies to FCR have been removed from the relevant packages.
	

None
glite-yaim-bdii 4.3.15-1 	EMI 3 SL5, EMI 3 SL6, EMI 2 SL5, EMI 2 SL6 	

BUG #17: New version of glite-yaim-bdii that sets the top BDII cache validity to 4 days by default (before was 12h) as this is believed to improve the overall caching mechanism available in the top BDII.
	

If you are interested in using the new cache validity default value, re-run yaim after the installation. Otherwise, no actions are needed.
bdii-config-top 1.0.10-1 	EMI 3 SL5, EMI 3 SL6, EMI 2 SL5, EMI 2 SL6 	

BUG #8: This release decommissions the FCR (Freedom of Choice of Resources) mechanism that is no longer needed in the top BDII. The dependencies to FCR have been removed from the relevant packages.
	

None
glue-validator-cron 1.3.0-1 	EMI 3 SL5, EMI 3 SL6, EMI 2 SL5, EMI 2 SL6 	

BUG #7: new version of glue-validator-cron that logs only the results for full EGI profile GLUE 2 validation.

 
	

None
Update: 4 - 07.10.2013 Name & Version 	Platform 	Release notes 	Installation & configuration
glue-validator 2.0.20-0 	EMI 2 SL5, EMI 2 SL6, EMI 3 SL5, EMI 3 SL6, UMD 2 SL5 (link is external), UMD 2 SL6 (link is external) 	

New version of glue-validator that will be validated by EGI for integration with the production Nagios infrastructure. This new version contains the final list of known issues affecting middleware providers that will allow the sites to execute the tool using the --exclude-known-issues option to focus only on errors related to site misconfiguration.
	

None
glite-info-provider-ldap 1.4.8-1 	EMI 2 SL5, EMI 2 SL6, EMI 3 SL5, EMI 3 SL6, UMD 2 SL5 (link is external), UMD 2 SL6 (link is external) 	

BUG #102698: Start with a clean cache directory in the case of Top BDII. This bug was preventing to publish some sites when the top BDII was performing slowly.

BUG #102675: Increase the default max size of LDIF files to 25MB

 
	

No BDII restart is needed.
glite-info-plugin-delayed-delete-status plugin 1.0.1-1 	EMI 2 SL5, EMI 2 SL6, EMI 3 SL5, EMI 3 SL6, UMD 2 SL5 (link is external), UMD 2 SL6 (link is external) 	

Fixed wrong attribute name 'GlueCEStatus' to 'GlueCEStateStatus' in the glite-info-plugin-delayed-delete-status plugin
	

No BDII restart is needed
Update: 3 - 09.09.2013 Name & Version 	Platform 	Release notes 	Installation & configuration
glite-info-provider-ldap 1.4.6-1 	EMI 2 SL5, EMI 2 SL6, EMI 3 SL5, EMI 3 SL6 	

BUG #102384: GLUE 2 Contact and Location objects are missing. This bug fix affects top BDIIs running versions 1.4.4-1 and 1.4.5-1 of the ldap information provider.
	

Restart the BDII
bdii 5.2.22-1 	EMI 2 SL5, EMI 2 SL6, EMI 3 SL5, EMI 3 SL6, EPEL 5 (link is external), EPEL 6 (link is external), UMD 2 SL5 (link is external), UMD 2 SL6 (link is external), UMD 3 SL5 (link is external), UMD 3 SL6 (link is external) 	

BUG #102506: Make /var/run/bdii configurable. This bug fix affects only ARC installations.
	

Restart the BDII
glue-validator 2.0.19 	EMI 2 SL5, EMI 2 SL6, EMI 3 SL5, EMI 3 SL6 	

New version of glue-validator containing a series of improvements and a new command line option called "--exclude-known-issues". This option allows system administrators to run glue-validator without testing those GLUE 2 attributes that are wrongly published due to known bugs in the middleware information providers.
	
Update: 2 - 05.08.2013 Name & Version 	Platform 	Release notes 	Installation & configuration
glite-info-provider-ldap 1.4.5-1 	EMI 2 SL5, EMI 2 SL6, EMI 3 SL5, EMI 3 SL6, UMD 3 SL5 (link is external), UMD 3 SL6 (link is external) 	

BUG #101805: Set to 'Unknown' ldap info provider cached state attributes for the site BDII and remove caching LDIF files in a top BDII.
	

This version affects site and top BDIIs where a restart of the BDII is needed.
glite-info-update-endpoints 2.0.13-1 	EMI 2 SL5, EMI 2 SL6, EMI 3 SL5, EMI 3 SL6, UMD 3 SL5 (link is external), UMD 3 SL6 (link is external) 	

BUG #99322: error message if manual file does not exist in the glite-info-update-endpoint configuration script
	

No special actions required.
bdii 5.2.21-1 	EMI 2 SL5, EMI 2 SL6, EMI 3 SL5, EMI 3 SL6, EPEL 5 (link is external), EPEL 6 (link is external), UMD 3 SL5 (link is external), UMD 3 SL6 (link is external) 	

    Fix for security vulnerability SVG-2013-5266 (link is external) (advisory released when this version of the bdii is released in UMD)
    BUG #102140: Start bdii-update daemon from "/"
    BUG #101709: Start bdii-update with -l option
    BUG #102014: clean site and top ldap info provider cache after a BDII restart
    BUG #101398: LDAP DB backend improvements for top BDII

	

A restart of the BDII is needed in all BDII flavors
bdii-config-top 1.0.8-1 	EMI 2 SL5, EMI 2 SL6 , EMI 2 SL5, EMI 2 SL6, UMD 3 SL5 (link is external), UMD 3 SL6 (link is external) 	

New dependecy and setup of the new plugin glite-info-plugin-delayed-delete-status.
	

The installation of this version will install the new package glite-info-plugin-delayed-delete-status in the top BDII.
glite-info-provider-service 1.13.1-1 	EMI 2 SL5, EMI 2 SL6, EMI 3 SL5, EMI 3 SL6, UMD 3 SL5 (link is external), UMD 3 SL6 (link is external) 	

    BUG #101562: Service information provider dies if it can't get a hostname
    BUG #100872: Service information provider updated to use new WMS rpm name
    BUG #100822: Service information provider change for Argus PDP endpoint
    BUG #100126: Service information provider change for new EMI 3 LB pid file
    BUG #102168: Service information provider change to set new limit of 240 chars to ServiceData strings

	

Restart the BDII to apply the fixes
glite-info-plugin-delayed-delete-status 1.0.0-1 	EMI 2 SL5, EMI 2 SL6, EMI 3 SL5, EMI 3 SL6, UMD 3 SL5 (link is external), UMD 3 SL6 (link is external) 	

A new plugin is responsible for publishing cached entries with value 'Unknown' in the corresponding GLUE state attributes of the top BDII.

BUG #99298: new plugin to set GLUE state attributes to 'Unknown' when the delayed delete option is configured
	

This is a new package that is installed as a dependency of bdii-config-top. A restart of the top BDII is needed to make use of the new plugin.
glite-yaim-bdii 4.3.14-1 	EMI 2 SL5, EMI 2 SL6, EMI 3 SL5, EMI 3 SL6, UMD 3 SL5 (link is external), UMD 3 SL6 (link is external) 	

BUG #101389: New YAIM parameter 'BDII_RAM_SIZE' that customises the RAM disk size for top BDII (Default is 1500M)
	

Reconfigure YAIM if the new variable BDII_RAM_SIZE is customised to a non default value.
Update: 1 - 31.05.2013 Name & Version 	Platform 	Release notes 	Installation & configuration
bdii 5.2.20-1 	EMI 3 SL5, EMI 3 SL6, EPEL 5 (link is external), EPEL 6 (link is external), UMD 3 SL5 (link is external), UMD 3 SL6 (link is external) 	

Bug fix release affecting all BDII flavours:

BUG #101237: Obsolete GLUE 2 entries were never removed from the BDII since the DNs were transformed into lower case and GLUE 2 is case sensitive. The correct case is now preserved and entries are properly deleted. This bug was affecting all BDII flavours.

BUG #101090: Missing symlink to a customised LDAP DB configuration file allowing for better performance tuning of the DB. The link was already available for GLUE 1 but not for GLUE 2. This should improve the performance of top BDIIs which can be otherwise degraded after GLUE 2 is wideliy published by all EGI sites.
	

After upgrading the bdii package, follow the instructions below:

Resource BDII

    restart BDII

Site BDII

    delete contents of /var/lib/bdii/gip/cache/gip/top-urls.conf-glue2
    restart BDII

Top BDII

    delete contents of /var/lib/bdii/gip/cache/gip/top-urls.conf-glue2
    restart BDII

glue-validator 2.0.17-0 	EMI 3 SL5, EMI 3 SL6, UMD 3 SL5 (link is external), UMD 3 SL6 (link is external) 	

New version of the glue-validator able to validate against the EGI profile and compatible with Nagios requirements. Check the GLUE validator guide for more details.
	
glue-validator-cron 1.2.0-1 	EMI 3 SL5, EMI 3 SL6, UMD 3 SL5 (link is external), UMD 3 SL6 (link is external) 	

The glue-validator-cron has been updated to use the new glue-validator command line options compatible with Nagios. glue-validator-cron now generates a log file for the validation against the EGI GLUE 2.0 profile.
