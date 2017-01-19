.. _tests:

Tests
=====

Level 0: Component
------------------

bdii
````

Run the test-bdii script found in the tests directory in SVN.

bdii-config-site
````````````````

Run the test-site-bdii script found in the test directory in SVN.

glite-info-provider-ldap
````````````````````````

Run the run-tests script found in the test directory in SVN.

glite-info-site
```````````````

Run the run-tests script found in the test directory in SVN.

glite-info-static
`````````````````

Run the run-tests.sh script found in the test directory in SVN.

glue-schema
```````````

Run the test-ldif.sh script found in the
`LDAP2 <http://glue.web.cern.ch/glue/glue/LDAP2/>`_ directory in OGF SVN mirror
at CERN.

gstat-validation
````````````````

No test currently available. This package contains tests itself.

gstat-web
`````````

Installation of gstat-dev and verification by manual inspection.

lcg-info
````````

Testing method unknown

lcg-infosites
`````````````

Testing method unknown

nagios-plugins-bdii
```````````````````

No test currently available. This package contains tests itself.

Level 1: Service Ping
---------------------

Site BDII
`````````

The package
`nagios-plugins-bdii <https://svnweb.cern.ch/trac/gridinfo/browser/nagios-plugins-bdii>`_
contains a probe check_bdii_entries that can be used to connect to the BDII and
measure the response time as well as the number of entries returned.
The
`gstat-validation <https://svnweb.cern.ch/trac/gridinfo/browser/gstat-validation>`_
contains probes that can be used to validate the information content.

Top BDII
````````

The package nagios-plugins-bdii contains a probe check_bdii_entries that can be
used to connect to the BDII and measure the response time as well as the number
of entries returned.

Level 2: Service Functionality
------------------------------

Site BDII
`````````

The service should be first installed using the prepare script and the
`test-BDII-site <https://svnweb.cern.ch/trac/gridinfo/browser/certification/>`_
script should be run.

Top BDII
````````

The service should be first installed using the prepare script and the
`test-BDII-top <https://svnweb.cern.ch/trac/gridinfo/browser/certification/>`_
script should be run.

Level 3: Service Performance and Stress Testing
-----------------------------------------------

The package `ldapbench <https://svnweb.cern.ch/trac/gridinfo/browser/ldapbench>`_
is used to stress and instance of the BDII. This is achieved by executing
multiple quires on a number of threads to generate a query load an measuring
the response time.

Level 4: Infrastructure
-----------------------

Infrastructure tests are part of the Staged Rollout activity managed by the EGI
project. For more information, please check the
`EGI Staged Rollout pages <https://wiki.egi.eu/wiki/Staged-Rollout>`_.
