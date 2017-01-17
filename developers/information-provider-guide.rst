Information Provider Guide
==========================

This guide explains how to create information provider for use with the BDII. It is intended to help developers create information providers for their specific service. Any questions, comments or suggests can be sent to the project-grid-info-support (link sends e-mail) email list.
GLUE 2.0

Any information published about the service must confirm to the GLUE 2.0 information model (link is external). This document contains a detailed description of the allowed attributes and attribute groupings. To compliment the specification, an LDAP rendering document ( doc (link is external) pdf (link is external) )is also available. Examples of the resulting LDIF file can be found here.
Before any attempt is made to create and information provider, it would be useful to become familiar with the GLUE 2.0 information model. It is also recommend to become familiar with LDAP (link is external) and LDIF (link is external).
LDIF, Provider or Plugin

An information provider and be provided in three different forms ( LDIF, provider, plugin) and the first step is to decide which should be used. It may be necessary to provide the information using a combination of all three.
A standalone LDIF file

An LDIF file should be used for static information that can be set during configuration time and will not change. This can contain default values and entires that my be overwritten by a provider or plugin.
Provider

An information provider is this is a script that returns LDIF to stdout.
Plugin

A plugin is a script that returns LDIF containing only LDAP modify statements. For more detail on the syntax see the man page of the ldapmodify command (link is external).

Examples of how LDIF files, plugins and providers work can be found here.
Integration with the BDII

The LDIF files, providers and plugins are deployed by placing them in the relevant directory as specified in the bdii.conf file. See the Resource BDII documentation for more details.
Testing

Use the glue-validator tool to make sure the information provider correctly generates GLUE1.3 and GLUE 2.0 information.

