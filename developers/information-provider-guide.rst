.. _information_provider_guide:

Information Provider Guide
==========================

This guide explains how to create information provider for use with the BDII.
It is intended to help developers create information providers for their
specific service. Any questions, comments or suggests can be sent to the
`project-grid-info-support <project-grid-info-support@cern.ch>`_ email list.

GLUE 2.0
--------

Any information published about the service must confirm to the
`GLUE 2.0 information model <http://www.ogf.org/documents/GFD.147.pdf>`_.
This document contains a detailed description of the allowed attributes and
attribute groupings. To compliment the specification, an LDAP rendering
document ( `doc <http://forge.gridforum.org/sf/go/doc15518?nav=1>`_
`pdf <http://forge.gridforum.org/sf/go/doc15526?nav=1>`_ )is also available.
Examples of the resulting LDIF file can be found
`here <http://glue.web.cern.ch/glue/glue/LDAP2/examples/>`_.

Before any attempt is made to create and information provider, it would be
useful to become familiar with the GLUE 2.0 information model. It is also
recommend to become familiar with
`LDAP <http://www.openldap.org/doc/admin22/intro.html#What%20is%20LDAP>`_ 
and
`LDIF <http://www.openldap.org/doc/admin22/dbtools.html#The%20LDIF%20text%20entry%20format>`_.

LDIF, Provider or Plugin
------------------------

An information provider and be provided in three different forms (*LDIF*,
*provider*, *plugin*) and the first step is to decide which should be used. It may
be necessary to provide the information using a combination of all three.

A standalone LDIF file
``````````````````````

An LDIF file should be used for static information that can be set during
configuration time and will not change. This can contain default values and
entires that my be overwritten by a provider or plugin.

Provider
````````

An information provider is this is a script that returns LDIF to stdout.

Plugin
``````

A plugin is a script that returns LDIF containing only LDAP modify statements.
For more detail on the syntax see the man page of the
`ldapmodify command <http://www.manpagez.com/man/1/ldapmodify/>`_.

Examples of how LDIF files, plugins and providers work can be found
`here <https://svnweb.cern.ch/trac/gridinfo/browser/bdii/trunk/tests>`_.

Integration with the BDII
-------------------------

The LDIF files, providers and plugins are deployed by placing them in the
relevant directory as specified in the bdii.conf file.
See the :ref:`resource_bdii` documentation for more details.

Testing
-------

Use the :ref:`glue_validator_guide` tool to make sure the information provider
correctly generates GLUE1.3 and GLUE 2.0 information.
