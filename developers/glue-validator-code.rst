.. _glue_validator_developers_guide:

GLUE Validator Developers Guide
===============================

Overview
--------

The GLUE Validator is a simple python-based unit test suite that validates
information against test cases. It works against both LDIF files and LDAP
servers. In addition, a GLUE 2.0 LDAP schema validator is available.

Installation
------------

To checkout the source code run the following command.

::

  svn co http://svn.cern.ch/guest/gridinfo/glue-validator/trunk

To install an rpm, run the following command.

::

  cd trunk; make clean rpm; rpm -Uvh build/RPMS/noarch/glue-validator-*-1.noarch.rpm ; cd -

For the glue2-schema-check, you will need to install the glue-schema and
openldap-servers packages.

Usage
-----

To see usage, run the following command.

::

  glue-validator

or

::

  glue-schema-validator

Alternatively, to run from source the PYTHONPATH will need to be set. This can
be achived by running the following command.

::

  export PYTHONPATH=${PYTHONPATH}:${PWD}/trunk/lib

Then the following command should work.

::

  ./trunk/bin/glue-validator

or

::

  ./trunk/bin/glue-schema-validator

Note For Ubuntu
```````````````

To get this working on Ubuntu you will need to disable apparmor for slapd.

::

  sudo ln -s /etc/apparmor.d/usr.sbin.slapd /etc/apparmor.d/disable/.
  sudo /etc/init.d/apparmor reload

To installed the glue-schema, run the following commands.

::

  svn co http://svn.cern.ch/guest/gridinfo/glue-validator/trunk
  cd trunk; make clean deb; dpkg -i build/glue-schema_*_all.deb ; cd -

Architecture
------------

The testing framework consists of two main parts, the main script and the
validator library.

The Main Scripts
````````````````

The purpose of the main script (glue-validator) is to parse the command line
arguments, read the LDIF/LDAP source, generate all the tests and to run the
test suite. To achieve these goals, it makes use of several libraries,
validator.utils and validator.*Test. The script iterates over each entry found
in the LDIF/LDAP source and for each entry adds a number of tests to the test
suite. After all the tests have been added, the test suite is run.

For all GLUE versions the main script runs validator.EntryTest. For the EGI
profile for GLUE 2, the glue-validator also runs validator.EGIProfileTest. This
library contains tests for each GLUE 2 attribute as described in the EGI
profile document.

The Libraries
`````````````

validator.utils
***************

This library is used to parse the command line options and read the LDIF/LDAP
source. It contains one or two tools for manipulating LDIF. It also contains
the code to generate nagios output and a function to display failure messages
in a standard way that could be then easily parsed. The internal structure of
storing entities is as follows.

::

  { dn : { attribute : [ value ]  }  }

validator.EntryTest
*******************

This library contains the EntryTest class, which extends the standard python
unittest.TestCase. This test class provides four tests; test_object_class,
test_mandatory_attributes, test_single_valued, test_data_types. This library
uses the data and types libraries from the test classes being used. One point
to note is that the test_data_types call a function with a dynamically name of
the format is_type, where the type is obtained from the data structure provided
by data  and the function is provided by the library types.

validator.EGIProfileTest
************************

This library contains the EGIProfileTest class, which also extends the standard
python unittest.TestCase. This test class provides one or more tests per GLUE 2
attribute. This library uses the data and types libraries from the egi-glue2
library where the EGI profile for GLUE2 definition in terms of attributes and
types is specified.

validator.WLCGTest
******************

This library contains specific tests from EGIProfileTest class thar are
particularly relevant to WLCG.

data.py
*******

This library essentially contains a description of the schema. The data
structure schema has the following format.

::

  { objectclass : { attribute : ( type, single_valued, mandatory ) } }

Where type is a string representing the data type of the attribute,
single_valued is a boolean indicating whether or not the attribute is single
valued and mandatory is a boolean indicating whether or not the attribute is
mandatory.

types.py
********

This library contains functions that test values and return True or False
depending on whether or not the input value conforms to that type.

validator.messages.py
*********************

This library contains the list of failure messages for Errors, Warnings and
Info messages. It is a dictionary containing the failure message code, its
description and the affected attribute.

validator.KnownIssues.py
************************

This library contains a list of the tests that are known to validate attributes
that are wrongly published by the BDII or the information providers. By
selecting the -k,--exclude-known-issues option in the command line, these tests
are not executed by the glue-validator.

Testing
```````

For each object class there should be a library of the form EntityTest.py.
These are the tests for the GLUE Validator suite and can be executed directly
and will be used for regression testing.
