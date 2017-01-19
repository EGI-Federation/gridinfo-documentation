.. _developers_guide:

Developers Guide
================

BDII is currently released in `UMD <http://repository.egi.eu/download/>`_
repositories and `EPEL repository <http://fedoraproject.org/wiki/EPEL>`_.

Communication
-------------

The `project-grid-info-devel <project-grid-info-devel@cern.ch>`_ email list is
used for communication between BDII developers. To join this list, fill in the
form on the `egroups subscription <https://e-groups.cern.ch/e-groups/Egroup.do?egroupId=171934>`_
page.

The `EGI URT <urt-discuss@mailman.egi.eu>`_ email list is used to plan UMD
releases. Make sure planned releases are announced with enough time in advance
at the `URT meetings <https://indico.egi.eu/indico/categoryDisplay.py?categId=107>`_.

Software Repository
-------------------

The CERN Subversion service is used for the software repository and can be
browsed using the SVN Browser. For write access to the repository, email the
*project-grid-info-devel* list.
The software can be checked out with the following command.

::

  svn co https://svn.cern.ch/reps/gridinfo/[COMPONENT]/trunk

For anonymous checkouts the following command can be used.

::

  svn co http://svn.cern.ch/guest/gridinfo/[COMPONENT]/trunk

COMPONENT refers to the concrete component you want to check out. Components
could be: bdii, gstat-web, etc. Example:

::

  svn co https://svn.cern.ch/reps/gridinfo/bdii/trunk

Version Control
---------------

To release a component it MUST be tagged with R_x_y_z, where x, y and z are the
major, minor and patch levels respectively. It must be ensured that the version
numbers for the package will agree with the svn tag and that they always
increase with newer versions! Tagging is achieved with the following command.

::

  svn copy https://svn.cern.ch/reps/gridinfo/example/trunk https://svn.cern.ch/reps/gridinfo/example/tags/R_x_y_z -m "New Release"

Building
--------

Packages released in the EMI 3 repositories MUST be built with the
`CERN koji <http://koji.cern.ch/koji/>`_ build system. Check the
`How to Build packages <https://twiki.cern.ch/twiki/bin/view/LinuxSupport/BuildingRPMswithKoji>`_
in the Agile Project Infrastructure to get a koji account and learn all the
details to use the CERN koji build system.

If a package is released for the first time, the following commands need to be executed:

::

  koji add-pkg --owner=malandes bdii6 package-name
  koji add-pkg --owner=malandes bdii6-testing package-name
  koji add-pkg --owner=malandes bdii6-stable package-name
  koji add-pkg --owner=malandes bdii7 package-name
  koji add-pkg --owner=malandes bdii7-testing package-name
  koji add-pkg --owner=malandes bdii7-stable package-name

The command to build the package in koji is:

::

  koji build bdii6 srpm-package
  koji build bdii7 srpm-package

If the build is successful the package will be available in the testing
repository `SL6 <http://linuxsoft.cern.ch/internal/repos/bdii6-testing>`_ and
`SL7 <http://linuxsoft.cern.ch/internal/repos/bdii6-testing>`_. In order to
install packages from the testing repository, use the following repo files
(Example below for SL6, please change bdii6 with bdii7 for the SL7 repo):

::

  [bdii6-testing]
  name=bdii6-testing
  baseurl=http://linuxsoft.cern.ch/internal/repos/bdii6-testing/$basearch/os/
  enabled=1
  gpgcheck=0
  priority=30

Testing and Quality Assurance
-----------------------------

Once the testing repository has been created, testing can begin. The testing
required is outlined in the :ref:`test_plan`. The tests described in the test
plan MUST be carried out for each component before it is considered for
release. The `CERN Openstack infrastructure <https://openstack.cern.ch/>`_
currently hosts the
`BDII testbed <https://gridinfo.web.cern.ch/sites/gridinfo.web.cern.ch/files/testbed.pdf#overlay-context=information-system-developers>`_.

It has to be noted as well that all the standard coding conventions should be
followed and installed software should use the directory structure as specified
in the `Filesystem Hierarchy Standard <http://www.pathname.com/fhs/>`_.
Packages should also be sanity checked before being moved into the testing
repository.

For integration testing with other middleware services, notify middleware
developers that a new BDII update is available in the testing repository
through the `EMI EMT <emt@eu-emi.eu>`_ mailing list.

For testing in production conditions, notify sites that are participating in
early evaluation that a new BDII update is available in the testing repository.
Release

Packages to be released in EMI 3 that have succesfully passed all tests can be
promoted to the stable repository by running:

::

  koji tag-pkg bdii6-stable package-name-version.el6
  koji tag-pkg bdii7-stable package-name-version.el7

This will create the packages also in the
`Linuxsoft <http://linuxsoft.cern.ch/internal/repos/>`_ repository.

The release should be announced and documented in the :ref:`bdii_releases`.
This page offers an RSS feed.

The corresponding JIRA and GGUS tickets that are fixed in the release, should
be closed including a link to the release notes.

This action MUST be accompanied with a notification to the
*EMI EMT* mailing list and the `URT <urt-discuss@mailman.egi.eu>`_
mailing list. The EMI and UMD release managers will take care of populating the
relevant repositories.  Note that only UMD releases are guaranteed by a
succesful `staged rollout <https://wiki.egi.eu/wiki/Staged_Rollout>`_

Defect Tracking
---------------

* The main entry point for users and system administrator is
  `GGUS <https://gus.fzk.de/ws/ticket_search.php>`_.
* GGUS notification are sent to the
  `project-grid-info-support <project-grid-info-support@cern.ch>`_ email list.
* Defects and enhancements are tracked using the
  `Grid Information System Jira <https://its.cern.ch/jira/plugins/servlet/project-config/GRIDINFO>`_
  tracker.

EPEL
----

BDII releases are also released in EPEL. In order to release a package in EPEL
you need to become a package maintainer. Find out more details in the following
links:

* How to get your
  `packager status <http://fedoraproject.org/wiki/EPEL_Package_Maintainers>`_
* Join the package collection
  `maintainers <https://fedoraproject.org/wiki/Join_the_package_collection_maintainers>`_
* How to get
  `sponsored <https://fedoraproject.org/wiki/How_to_get_sponsored_into_the_packager_group>`_
  into the packager group
* `Package review process <https://fedoraproject.org/wiki/Package_Review_Process>`_

The status of EPEL releases for the BDII is sumarised in this twiki. For
further details, please use the
`Fedora Package database <https://admin.fedoraproject.org/pkgdb>`_.
