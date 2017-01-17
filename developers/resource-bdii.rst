Resource BDII
=============

The resource-level BDII is an instance of the BDII that contains information about a Grid Service and is typically deployed with the service itself. It consists of an OpenLDAP database that is periodically updated by a parallel process that obtains information about the Grid Service from one or more information sources. For more detailed information about the BDII, please read the Information System Introduction. All services MUST publish their existence in both the GLUE 1.3 (link is external) and GLUE 2.0 data models.

For any further questions, please contact project-grid-info-support (link sends e-mail).
Installation

To provide a resource-level BDII, a dependecy must be set on the following rpms:

    bdii
    glue-schema
    glite-info-provider-service

The latest version is available in the EMI repositories.
Configuration

The BDII should need no further configuration, however, information on the configuration parameters used by the BDII are described in the BDII quickstart guide. The service can be started with the following command.

/sbin/service bdii start

Information Provider Setup

By default, the BDII uses the following three directories to obtain information sources.

/var/lib/bdii/gip/ldif
/var/lib/bdii/gip/provider
/var/lib/bdii/gip/plugin

These directories are specified as configuration parameters in the BDII's configuration. Static LDIF files should be placed in the ldif directory, information providers should be put in the providers and information plugins should be put in the plugin directory.
Service Information Provider

By default, all services should publish themselves by using the service information provider package. A number of template configuration files for some services can be found in /etc/glite/info/service. If a template file can be used, a configuration file can be created by running the following command.

cp  /etc/glite/info/service/glite-info-service-xxx.conf.template /etc/glite/info/service/glite-info-service-xxx.conf

where xxx is the name of the service. The file may need to be edited to include information which is only available at configuration time, e.g. the list of supported VOs.

The service information provider can be added by creating a wrapper script in the _provider'' directory.

cat  << EOF > /var/lib/bdii/gip/provider/glite-info-provider-service-xxx
#!/bin/sh
/usr/bin/glite-info-service /etc/glite/info/service/glite-info-service-xxx.conf MYSITE
/usr/bin/glite-info-glue2-simple /etc/glite/info/service/glite-info-service-xxx.conf MYSITE
EOF

chmod +a /var/run/bdii/gip/provider/glite-info-provider-service-xxx

where xxx is the name of the service. Environment variables can be set to be used in the provider and MYSITE is the GlueSiteUnqiueID. More details on the service information provider can be found in the README and README-GLUE2 file.
Service Specific Information Providers

For any other service specific information, LDIF file, information providers and plugins may need to be created and placed into the respective directories. For further advice on what is required for a specific service, please contact project-grid-info-support (link sends e-mail).
Testing

Basic testing can be achieved by doing an ldapsearch and looking at the output.
Test that the BDII is operational

ldapsearch -x -h $(hostname) -p 2170 -b o=infosys

Test that the BDII is updating

ldapsearch -x -h $(hostname) -p 2170 -b o=infosys "*" modifyTimestamp

Test that the Glue 1.3 root entry is available

ldapsearch -x -h $(hostname) -p 2170 -b mds-vo-name=resource,o=grid

Test that the Glue 2.0 root entry is available

ldapsearch -x -h $(hostname) -p 2170 -b o=glue

GLUE Validation tests

The Glue Validator should also be used to test for GLUE 1.x and GLUE 2.0 conformance.

