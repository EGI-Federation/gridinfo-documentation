Known Issues
============

Resource BDII
-------------

**Important note: site and top BDIIs are also affected by any known issues in the resource BDII.**

* `BUG #GRIDINFO-57 <https://its.cern.ch/jira/browse/GRIDINFO-57>`_: Affects all
  versions of the bdii. When a DN changes its case from lower to upper case or
  viceversa, these changes are not propagated to the BDII and the new DN doesn't
  get published. This only affects GLUE 2 because it's case sensitive. The
  workaround is to add an extra difference like a "_" or "-" or anthing else, so
  that the BDII is able to see the DN is a new one and like this it will get
  published.

* Affects when upgrading to bdii >= 5.2.20-1 using EPEL 5 (SL5 installations)
  repository. In this scenario, the LDAP daemon fails to start. YAIM detects that
  Openldap 2.4 is installed and tries to use it. On the other hand, the
  slapd.conf file has been defined to use Openldap 2.3. This is because Openldap
  2.4 is not distributed in EPEL 5 and the necessary dependencies have been
  resolved with Openldap 2.3 packages. Please, uninstall openldap2.4-* packages
  or add the following lines in /etc/bdii/bdii-slapd.conf:

::

  modulepath /usr/lib64/openldap2.4
  moduleload back_relay

* Affects when upgrading to bdii >= 5.2.17-1 using EMI or UMD SL5 repositories:
  Openldap 2.4 is the mandatory version needed since the EMI 3 release. This is
  due to some changes in the configuration of the BDII needed to be able to work
  with ARC resources. If YAIM is not used to configure the BDII, the
  /etc/sysconfig/bdii file needs to be manually changed and define:

::

  SLAPD=/usr/sbin/slapd2.4

* Empty attributes are no longer allowed in the GLUE 2.0 schema. The
  corresponding object will not be published if at least one attribute is empty.

* `BUG #101709 <http://savannah.web.cern.ch/savannah/EGEE/jra1mdw/bugs/101709.html>`_: Affects
  bdii < 5.2.21-1. At boot time or when using 'service bdii restart', the
  environment is reset and some information providers (i.e. the ones for SGE
  batch system) fail due to missing environment varibles, publishing default
  values in the BDII.
  * *Workaround*: use '/etc/init.d/bdii restart' since this preserves the environment.
* `BUG #101237 <https://savannah.cern.ch/bugs/?101237>`_: Affects bdii <
  5.2.20-1. Obsolete GLUE 2 entries are not removed due to a bug in the delete
  functionality of the BDII.

  * *Workaround*: clean the cache used by the glite-info-provider-ldap script
    and restart all the BDIIs in the site:

    * Restart resource BDIIs
    * Remove contents of /var/lib/bdii/gip/cache/gip/site-urls.conf-glue2/ and restart site BDII
    * Remove contents of /var/lib/bdii/gip/cache/gip/top-urls.conf-glue2/ and restart the top BDII

Top BDII
--------

* `BUGZILLA <https://bugzilla.redhat.com/show_bug.cgi?id=1257543>`_: Slapd
  process on Top BDII crashes after upgrade to CentOS/SLC6.7 with
  openldap-servers-2.4.40-5.el6.

* Affects glite-info-plugin-delayed-delete-status 1.0.0-1: If a resource BDII
  or OSG resource is down for a while, its status attributes (like
  GlueCEStateStatus, GlueServiceStatus, GlueServiceStatus or GlueSEStatus, and
  the same for GLUE 2) published across top BDIIs may not match. All top BDIIs
  should run at least glite-info-plugin-delayed-delete-status 1.0.1-1 to get rid
  of this issue. Note that Top BDIIs runinng version 1.0.1-1 of the plugin would
  publish status 'Unknown', while previous ones would publish the last published
  status before the resource disappeared (although it is also possible that they
  publish status 'Unknown' if this value propagated from their site BDII before
  the resource dissapears from the site BDII cache).

  * *Workaround*: The root cause should be fixed at infrastructure level. In
    the meantime, the sys admin of the affected resource could at least make sure
    the resource is back to be published in the corresponding site BDII.

* `BUG #102608 <https://savannah.cern.ch/bugs/index.php?102608>`_: Affects
  1.4.7-1 > glite-info-provider-ldap >= 1.4.5-1. Sites dissapear from the top
  level BDII after the BDII_DELETE_DELAY is over.

  * *Workaround*: Increase the cache validity in
    /usr/libexec/glite-info-provider-ldap, line 122 (there is no need to restart
    the BDII):

::

  $ttl=300;


* `BUG #102384 <https://savannah.cern.ch/bugs/index.php?102384>`_: Affects bdii
  >= 5.2.17-1 and ldap-info-provider-ldap < 1.4.6-1 GLUE 2 Contact and Location
  objects are not published in the top level BDII. Although the effect of this
  bug is visible in top level BDIIs, this bug requires a fix in the site BDIIs.
  No workaround is suggested for this bug since it has to be applied in all site
  BDIIs which are not under the control of the top BDII sys admin.

* `BUG #GRIDINFO-4 <https://its.cern.ch/jira/browse/GRIDINFO-4>`_:
  glite-info-plugin-delayed-delete-status does not set to 'Unknown' Coputing and
  Storage Share state attributes

* The glite-info-update-endpoints script is executed as an hourly cron job. It
  creates a cache file of the list of GOCDB and OIM site LDAP URLs. When the BDII
  is restarted, the cache file is used. Although the list of sites does not
  change very frequently in GOCDB and OIM, for an up to date list, re-run
  glite-info-update-endpoints before the BDII restart:

::

  /usr/bin/glite-info-update-endpoints -c /etc/glite/glite-info-update-endpoints.conf

* `BUG #99298 <https://savannah.cern.ch/bugs/?99298>`_: Affects bdii < 5.2.21-1.
  Due to the caching mode, decommissioned services are published as 'Production'
  until the cache expires.  They should instead be published as 'Unknown'.

* `BUG #99322 <https://savannah.cern.ch/bugs/?99322>`_: Affects
  glite-info-update-endpoints < 2.0.13-1. The glite-info-update-endpoints script
  does not fail when using the manual option and the input file does not exist.

* `BUG #101090 <https://savannah.cern.ch/bugs/?101090>`_: Affects bdii <
  5.2.20-1. The GLUE 2.0 database backend in the LDAP server is not benefitting
  from a set of performance improvements due to a missing symlink to the proper
  configuration file.

  * *Workaround*: edit /etc/init.d/bdii and add in line 150:

::

  $RUNUSER -s /bin/sh ${BDII_USER} -c "ln -sf ${DB_CONFIG}_top ${SLAPD_DB_DIR}/glue/DB_CONFIG"

Site BDII
---------

* Upgrade to openldap-2.4.40-12 on SL6: if clients experience slow queries, a reboot of the node solves the issue.

* `BUG #GRIDINFO-5 <https://its.cern.ch/jira/browse/GRIDINFO-5>`_: Sometimes
  GLUE state attributes are not cleanly replaced with the string 'Unknown'. i.e.
  "GLUE2EndpointHealthStateInfo: Unknownp and running"

Information Providers
---------------------

PBS/Torque
``````````

* `CREAM-101 <https://issues.infn.it/jira/browse/CREAM-101>`_: Fixed in EMI 2
  Update 16 and EMI 3 Update 6. Wallclock time is published in hours when GLUE 1
  attributes should be expressed in minutes and GLUE 2 attributes should be
  expressed in seconds. See the
  `CREAM Known Issues <https://wiki.italiangrid.it/twiki/bin/view/CREAM/KnownIssues#Wrong_time_format_for_MaxWallClo>`_
  page for the details and the workaround.

