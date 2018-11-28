.. _bdii_releases:

BDII Releases
=============

Update: Update 11 - 28.11.2018

+-----------------------------------+---------------+-----------------------------------------------------------------------------+------------------------------------+
| Name & Version                    | Platform      | Release notes                                                               | Installation & configuration       |
+===================================+===============+=============================================================================+====================================+
| glite-info-update-endpoints 3.0.1 | SL6, CentOS 7 | - #1: Fix silent fail on CentOS 7 when unable to validate GOCDB certificate | Check configuration changes.       |
|                                   |               | - #11: Totally drop OSG support                                             |                                    |
|                                   |               | - #17: Handle sane defaults in the configuration file                       |                                    |
|                                   |               | - PR#14: Linting and build in containers                                    |                                    |
+-----------------------------------+---------------+-----------------------------------------------------------------------------+------------------------------------+
| bdii 5.2.25                       | SL6, CentOS 7 | - #3: Fix restart failing on stale PID                                      | Restart to use new init script.    |
|                                   |               | - PR#9: import BDII product card JSON                                       |                                    |
|                                   |               | - PR#11: Linting and build in containers                                    |                                    |
+-----------------------------------+---------------+-----------------------------------------------------------------------------+------------------------------------+

Update: Update 10 - 06.10.2014

+-----------------------+----------+-----------------------------------------------------------------------+------------------------------------+
| Name & Version        | Platform | Release notes                                                         | Installation & configuration       |
+=======================+==========+=======================================================================+====================================+
| glue-validator 2.0.25 | SL5, SL6 | #GRIDINFO-58: new version of glue-validator which applies an internal | Note that glue-validator is        |
|                       |          | workaround for not testing the Admin Foreign Key attributes in the    | integrated as a Nagios Operational |
|                       |          | case of StoRM services as there is a known bug in the information     | probe for EGI for the automatic    |
|                       |          | provider that prevents from publishing correct information.           | validation of GLUE 2 data.         |
+-----------------------+----------+-----------------------------------------------------------------------+------------------------------------+

Update: Update 9 - 07.08.2014

+-----------------------------+------------+-------------------------------------------------------------------------+--------------------------------------------+
| Name & Version              | Platform   | Release notes                                                           | Installation & configuration               |
+=============================+============+=========================================================================+============================================+
| glue-schema 2.0.11-1        | EMI 3 SL5, | Update of the GLUE 2 schema LDAP definition with the following changes: | A BDII restart is needed to be             |
|                             | EMI 3 SL6  | GRIDINFO-53: All the entities but Entity moved to type STRUCTURAL       | able to use the new GLUE 2 schema          |
|                             |            | GRIDINFO-9: GLUE 2 booleans should be DirectoryString not LDAP Boolean  | revision.                                  |
|                             |            |                                                                         |                                            |
|                             |            | Note that the change regarding the boolean attributes affects in        |                                            |
|                             |            | particular the following attributes:                                    |                                            |
|                             |            | GLUE2ExecutionEnvironmentVirtualMachine,                                |                                            |
|                             |            | GLUE2ExecutionEnvironmentConnectivityIn,                                |                                            |
|                             |            | GLUE2ExecutionEnvironmentConnectivityOut, GLUE2AdminDomainDistributed,  |                                            |
|                             |            | GLUE2ComputingManagerBulkSubmission, GLUE2ComputingManagerHomogeneous,  |                                            |
|                             |            | GLUE2ComputingManagerWorkingAreaGuaranteed,                             |                                            |
|                             |            | GLUE2ComputingManagerWorkingAreaShared.                                 |                                            |
|                             |            | The change refers to:                                                   |                                            |
|                             |            | The BooleanMatch has been removed from the schema. All booleans are     |                                            |
|                             |            | strings now.                                                            |                                            |
|                             |            |                                                                         |                                            |
|                             |            | Booleans are now DirectoryString type as well. This means that if the   |                                            |
|                             |            | attribute has no value, the attribute will not be published. It also    |                                            |
|                             |            | means that the boolean is expected to be as defined in GFD.147 section  |                                            |
|                             |            | A.3, that is, might contain the value "undefined" when not "true" nor   |                                            |
|                             |            | "false".                                                                |                                            |
+-----------------------------+------------+-------------------------------------------------------------------------+--------------------------------------------+
| glite-info-provider-service | EMI 3 SL5, | New version of the info provider fixing a bug and publishing a new      | The CREAM CE, site BDIIs and top BDIIs are |
| 1.13.4-1                    | EMI 3 SL6  | attribute:                                                              | the only services affected by this new     |
|                             |            | GGUS:107264 (link is external): Patch for the RTEPublisher start time   | release. No restart or reconfiguration of  |
|                             |            | GRIDINFO-54: New attribute to print GLUE schema version                 | the BDII is needed in any case.            |
+-----------------------------+------------+-------------------------------------------------------------------------+--------------------------------------------+
| glue-validator 2.0.24-1     | EMI 3 SL5, | Minor release containing an update of the types.py library and the      | Note that glue-validator is integrated as  |
|                             | EMI 3 SL6  | deprecation of one of the tests as requested by EGI:                    | a Nagios Operational probe for EGI for the |
|                             |            | GRIDINFO-52: xroot should be used when referring to the xrootd protocol | automatic validation of GLUE 2 data. Note  |
|                             |            | GRIDINFO-51: Add new ServiceType values                                 | that this particular version of            |
|                             |            | GRIDINFO-50: Obsolete WLCG_NAME test                                    | glue-validator has not been deployed in    |
|                             |            | GRIDINFO-47: Add 'notification' in the capability type                  | Nagios due to a bug in StoRM that raises   |
|                             |            | GRIDINFO-46: Bugs reported by DPM (II)                                  | an ERROR for sites (GGUS:108556). The fix  |
|                             |            | GRIDINFO-6: Test mandatory objects are present                          | is required in the info provider. a new    |
|                             |            | GRIDINFO-3: Test GLUE2ServiceAdminDomainForeignKey = GLUE2DomainID in   | glue-validator version will be provided to |
|                             |            | the DN                                                                  | workaround this issue.                     |
+-----------------------------+------------+-------------------------------------------------------------------------+--------------------------------------------+
| bdii 5.2.23-1               | EMI 3 SL5, | GRIDINFO-55: Number of parallel threads set to 64 by default to be able | Only top BDIIs are affected by this fix.   |
|                             | EMI 3 SL6  | to cope with high load scenarios as the one reported in GGUS:107621.    | A restart of the BDII is needed after      |
|                             |            |                                                                         | upgrading the package.                     |
+-----------------------------+------------+-------------------------------------------------------------------------+--------------------------------------------+
