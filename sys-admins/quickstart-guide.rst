.. _quickstart_guide:

Quickstart guide
================

Configuration
-------------

The configuration file used to configure the BDII itself is
/etc/bdii/bdii.conf. The format is key/value pairs with an '=' sign as the
separator. A default configuration file comes with the BDII. This may require
editing in order for the BDII to function as desired. The table belows
describes the key/value pairs found in the configuration file.

+-------------------+-------------------------------+-------------------------------------------------------------------------------+
| Key               | Typicaly Value                | Description                                                                   |
+===================+===============================+===============================================================================+
| BDII_LOG_FILE     | /var/log/bdii/bdii-update.log | The log file for the BDII update process                                      |
+-------------------+-------------------------------+-------------------------------------------------------------------------------+
| BDII_PID_FILE     | /var/run/bdii/bdii-update.pid | PID file for the bdii-update daemon                                           |
+-------------------+-------------------------------+-------------------------------------------------------------------------------+
| BDII_LOG_LEVEL    | ERROR                         | The log level for the update process [ERROR, WARNING, INFO, DEBUG ]           |
+-------------------+-------------------------------+-------------------------------------------------------------------------------+
| BDII_LDIF_DIR     | /var/lib/bdii/gip/ldif        | The directory containing LDIF files                                           |
+-------------------+-------------------------------+-------------------------------------------------------------------------------+
| BDII_PROVIDER_DIR | /var/lib/bdii/gip/provider    | The directory containing information providers                                |
+-------------------+-------------------------------+-------------------------------------------------------------------------------+
| BDII_PLUGIN_DIR   | /var/lib/bdii/gip/plugin      | The directory containing plugins                                              |
+-------------------+-------------------------------+-------------------------------------------------------------------------------+
| BDII_PORT         | 2170                          | The port which is used for the LDAP server                                    |
+-------------------+-------------------------------+-------------------------------------------------------------------------------+
| BDII_VAR_DIR      | /var/lib/bdii                 | The directory to use by the BDII for writing data                             |
+-------------------+-------------------------------+-------------------------------------------------------------------------------+
| BDII_BREATHE_TIME | 120                           | Time to wait before updating the next database                                |
+-------------------+-------------------------------+-------------------------------------------------------------------------------+
| BDII_READ_TIMEOUT | 300                           | Time to wait for LDAP sources to return                                       |
+-------------------+-------------------------------+-------------------------------------------------------------------------------+
| BDII_ARCHIVE_SIZE | 0                             | The number of updates that the changes should be logged                       |
+-------------------+-------------------------------+-------------------------------------------------------------------------------+
| BDII_USER         | ldap                          | The user runing the update process and the slapd databases                    |
+-------------------+-------------------------------+-------------------------------------------------------------------------------+
| BDII_DELETE_DELAY | 43200                         | Time to wait in seconds before deleting removed entries. Default is 12 hours. |
|                   |                               | This variable enables the caching mode. For disabling it set it to 0.         |
+-------------------+-------------------------------+-------------------------------------------------------------------------------+

Starting and Stopping the BDII
------------------------------

The BDII is started and stopped by the daemon script /etc/init.d/bdii. The
following commands can be used:

::

  service bdii start
  service bdii stop

File Locations and Descriptions
-------------------------------

The following table contains a list of files and locations which may be useful
during troubleshooting.

+-------------------------------------+-----------------------------------------------+
| Location                            | Description                                   |
+=====================================+===============================================+
| /etc/bdii/bdii.conf                 | BDII configuration file                        |
+-------------------------------------+-----------------------------------------------+
| /etc/bdii/bdii-(top-)slapd.conf     | The slapd.conf template for use with the bdii |
+-------------------------------------+-----------------------------------------------+
| /var/lib/bdii/gip/ldif/default.ldif | A default LDIF file to populate the bdii      |
+-------------------------------------+-----------------------------------------------+
| /etc/init.d/bdii                    | BDII init.d script                            |
+-------------------------------------+-----------------------------------------------+
| /usr/sbin/bdii-update               | Main update script                            |
+-------------------------------------+-----------------------------------------------+
| /opt/bdii/bin/bdii-proxy            | Creates proxy for the BDII                    |
+-------------------------------------+-----------------------------------------------+
| /var/log/bdii/bdii-update.log       | The BDII log file                             |
+-------------------------------------+-----------------------------------------------+
| /var/run/bdii-update.pid            | Te bdii-update.pid of the main process        |
+-------------------------------------+-----------------------------------------------+

Running Processes
-----------------

When a BDII is started, the following processes run:

* One multithreaded slapd process.The number of (active) threads may depend on
  the query load and/or the /opt/bdii/etc/bdii-slapd.conf file.
* 1 bdii-update process.
* Periodically, one ldapadd, ldapdelete or ldapmodify process.
