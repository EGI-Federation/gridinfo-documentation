.. _ginfo:

ginfo
=====

ginfo is a client tool for GLUE 2.0. It queries information from the BDII and
lists the attributes corresponding to an object. By default, all the attributes
of an object are displayed.

ginfo is available in `EPEL 5
<http://dl.fedoraproject.org/pub/epel/5/x86_64/repoview/ginfo.html>`_ and
`EPEL 6 <http://dl.fedoraproject.org/pub/epel/6/x86_64/repoview/ginfo.html>`_
repositories.

Usage
-----

::

  ginfo   [options]   Object   [attribute_to_filter='value of the attribute']   [attribute_to_display]

Only the object is mandatory.

Options:
````````

::

  -H,   --host  host        Specify a host to query. By default the environmental variable LCG_GFAL_INFOSYS will be used.
  -b,   --bind  binding     Specify the binding (o=glue by default).
  -l,   --list  attribute   List all the possible values of the specified attribute.
  -c,   --csv               Output in CSV format
  -j,   --json              Output in JSON format
  -t,   --timeout           Change the ldap timeout (15 seconds by default).
  -v,   --verbose           Enable verbose mode
  -V,   --version           Print the version of ginfo
  -h     --help             Print this helpful message

Objects and corresponding attributes:
`````````````````````````````````````

+----------------------+-----------------------------------------------------------------+
| Object               | Attributes                                                      |
+======================+=================================================================+
| AdminDomain          | ID, Description.                                                |
+----------------------+-----------------------------------------------------------------+
| ComputingManager     | ID, ProductName, ProductVersion, ServiceID.                     |
+----------------------+-----------------------------------------------------------------+
| ComputingShare       | ID, MaxCPUTime, MaxWallTime, ServingState,                      |
|                      | ExecutionEnvironmentForeignKey, RunningJobs, WaitingJobs.       |
+----------------------+-----------------------------------------------------------------+
| Endpoint             | ID, URL, Capability, InterfaceName, InterfaceVersion,           |
|                      | Implementor, ImplementationVersion, QualityLevel,               |
|                      | HealthState, ServingState, ServiceForeignKey.                   |
+----------------------+-----------------------------------------------------------------+
| ExecutionEnvironment | ID, OSName, ConnectivityOut, MainMemorySize, VirtualMemorySize. |
+----------------------+-----------------------------------------------------------------+
| Location             | ID, Country, Latitude, Longitude.                               |
+----------------------+-----------------------------------------------------------------+
| MappingPolicy        | ID, Scheme, Rule, ComputingShareID.                             |
+----------------------+-----------------------------------------------------------------+
| Service              | ID, Capability, Type, QualityLevel, StatusInfo, AdminDomainID.  |
+----------------------+-----------------------------------------------------------------+

Output Format
-------------

Standard output for an Endpoint:
````````````````````````````````

::

  HealthState: Value
  Implementor: Value
  InterfaceName: Value
  ServingState: Value
  URL: Value
  ImplementationVersion: Value
  Capability: Value
  ServiceForeignKey: Value
  QualityLevel: Value
  ID: Value
  InterfaceVersion: Value

JSON output for an Endpoint:
````````````````````````````

::

  [... "Value_of_the_ID": {
  "HealthState": Value,
  "Implementor": Value,
  "InterfaceName": Value,
  "ServingState": Value,
  "URL": Value,
  "ImplementationVersion": Value,
  "Capability": Value,
  "ServiceForeignKey": Value,
  "QualityLevel": Value,
  "ID": Value,
  "InterfaceVersion": Value}, ...]

CSV output for an Endpoint:
```````````````````````````

::

  HealthState,Implementor,InterfaceName,ServingState,URL,ImplementationVersion,Capability,ServiceForeignKey,QualityLevel,ID,InterfaceVersion


Examples
--------

* List all information for all Endpoint attributes:

  ::

    ginfo --host bdii.example.com Endpoint

* Use the host from the LCG_GFAL_INFOSYS environment variable and list all
  Location countries:

::

  export LCG_GFAL_INFOSYS=bdii.example.com:2170
  ginfo Location country

* List all the Service types:

::

  ginfo -l Type Service

* List all IDs from Endpoint which  have  'org.glite.FileTransfer'  as name of
  Interface:

::

  ginfo Endpoint InterfaceName=org.glite.FileTransfer ID

* Show the version too:

::

    ginfo Endpoint  InterfaceName=org.glite.FileTransfer  ID  InterfaceVersion

* Show all available information about these Endpoints:

::

  ginfo Endpoint InterfaceName=org.glite.FileTransfer

* Export to CSV:

::

  ginfo --csv Endpoint InterfaceName=org.glite.FileTransfer

Support
-------

In case of problems, please open a `GGUS <https://ggus.eu/pages/ticket.php>`_ ticket.

