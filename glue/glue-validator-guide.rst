GLUE validator guide
====================

The glue-validator command is a very useful command for system administrators
and middleware developers who want to validate whether the information
published by the service they are managing or developing is compliant with Glue
2.0 and Glue 1.3. For more information about the GLUE schema, please visit the
`GLUE <http://gridinfo.web.cern.ch/glue>`_ section in this web.

The glue-validator is also able to validate against the
`EGI profile for Glue 2.0 <http://go.egi.eu/glue2-profile>`_. This is the
recommended and default validation as it specifies how the Glue 2.0 information
schema should be used in EGI. The EGI profile gives detailed guidance on what
should be published, how the information should be interpreted, what kinds of
uses are likely and how the information may be validated to ensure accuracy.

Glue-validator Error Codes
--------------------------

Check the glue-validator
`error codes <http://twiki.cern.ch/twiki/bin/view/EGEE/GLUEValidatorErrorCodes>`_
containing tips to fix the errors.


** Important Note: This user guide documments glue-validator version >= 2.0.20.**

Support
-------

Please, use `GGUS <https://ggus.org/>`_ for any enquiry related to the
glue-validator and also to report any incident.

Quickstart guide
----------------

The glue-validator can be downloaded from CERN Linuxsoft
(`SL5 <http://linuxsoft.cern.ch/internal/repos/bdii5-stable>`_ and
`SL6 <http://linuxsoft.cern.ch/internal/repos/bdii6-stable>`_)
repository and also `EMI 3 <http://emisoft.web.cern.ch/emisoft/>`_ repository
(Bear in mind that EMI 3 repository is updated once per month and there may be
some delay to propagate the very last version there).

The glue-validator command is used in the following way:

::

  Usage: ./glue-validator [LDIF OPTIONS] [-g] [-s] [Other Options]

  Mandatory Arguments:

  Server Mode: Obtains LDIF from an OpenLDAP server
   -H --hostname      Hostname of the LDAP server
   -p --port          Port for the LDAP server
   -b --bind          The bind point for the LDAP server

  File Mode: Obtains LDIF directly from a file
   -f --file          An LDIF file

  Optional Arguments:

  GLUE version: Selects the GLUE schema version to be tested
   -g --glue-version        The glue schema version to be tested [glue1|glue2|egi-glue2 (default)]

  Tesuite type: Selects the set of tests to be executed against the LDIF
   -s --testsuite     The testsuite  [general|egi-profile (default)]

  Other Options:
   -k --exclude-known-issues  Do not run tests for wrongly published attributes due to known bugs
   -t --timeout               glue-validator runtime timeout, default 10s
   -v --verbose               Verbosity level 0-3, default 1
   -r --separator             Defines the separator for the output messages, default \n
                              This is only available for the verbosity level 3.
   -V --version               Prints glue-validator version
   -h --help                  Prints glue-validator usage

Examples:
`````````

* EGI profile against GLUE 2.0 validation: 

::

  glue-validator -H localhost -p 2170 -b o=glue 

* GLUE 1.3 validation:

::

  glue-validator -H localhost -p 2170 -b o=grid -g glue1 -s general

* GLUE 2.0 validation:

::

  glue-validator -H localhost -p 2170 -b o=glue -g glue2 -s general


By default, the output of the command reports a summary with the number of
Errors, Warning and Info messages.

The command can be run with -n option which allows for 3 different verbosity
levels. Level 1 is the output explained in the previous paragraph; Level 2 is a
summary per error, warning and info messages; Level 3 gives more details for
each message.

The messages for the EGI profile for GLUE 2 validation are documented in detail
in the following `twiki page <https://twiki.cern.ch/twiki/bin/view/EGEE/GLUEValidatorErrorCodes>`_.

EGI profile for GLUE 2.0 compliance
-----------------------------------

To validate against the EGI profile for GLUE 2.0, the following command must be
run, replacing the site-bdii.host and port with the hostname and port of the
site BDII:

::

  glue-validator -H site-bdii.host -p port -b o=glue

Note that in this example the validation is done at site level but it can be
done at any level.

Querying a site may take some time, in some cases it is necessary to define the
-t option with a reasonable timeout value to leave the site BDII enough time to
respond to the query.

When validating against the EGI profile for GLUE 2.0 it is recommended to
choose Nagios output and verbose level of '3' for all the details, otherwise
'2' for a summary of the encountered problems.

If the validation is done by a site admin, it is recommended to run the tool
using the option --exclude-known-issues. This option will not run tests to
variables that are wrongly published due to known bugs in the middleware
information providers:

::

  glue-validator -H site-bdii.host -p port -b o=glue --exclude-known-issues

Tips to know what to do to fix the errors reported by glue-validator can be
found in this `twiki <https://twiki.cern.ch/twiki/bin/view/EGEE/GLUEValidatorErrorCodes>`_.

Glue 2.0 compliance
-------------------

To test GLUE 2.0 information, the following command must be run, replacing the
site-bdii.host and port with the hostname and port of the site BDII.

::

  glue-validator -g glue2 -H site-bdii.host -p port -b o=glue -s general

Note that in this example the validation is done at site level but it can be
done at any level.

Glue 1.3 compliance
-------------------

To test GLUE 1.3 information, the following command must be run, replacing the
site-bdii.host and port with the hostname and port of the site BDII.

::

  glue-validator -g glue1 -H site-bdii.host -p port -b o=grid -s testsuite

Note that in this example the validation is done at site level but it can be
done at any level.
