Developers Guide
================

BDII is currently released in UMD (link is external) repositories and EPEL (link is external).
Communication

The project-grid-info-devel (link sends e-mail) email list is used for communication between BDII developers. To join this list, fill in the form on the egroups subscription page.

The EGI URT (link sends e-mail) email list is used to plan UMD releases. Make sure planned releases are announced with enough time in advance at the URT meetings (link is external).
Software Repository

The CERN Subversion service is used for the software repository and can be browsed using the SVN Browser. For write access to the repository, email the project-grid-info-devel (link sends e-mail) list. The software can be checked out with the following command.

svn co https://svn.cern.ch/reps/gridinfo/[COMPONENT]/trunk

For anonymous checkouts the following command can be used.

svn co http://svn.cern.ch/guest/gridinfo/[COMPONENT]/trunk

COMPONENT refers to the concrete component you want to check out. Components could be: bdii, gstat-web, etc. Example:

svn co https://svn.cern.ch/reps/gridinfo/bdii/trunk

Version Control

To release a component it MUST be tagged with R_x_y_z, where x, y and z are the major, minor and patch levels respectively. It must be ensured that the version numbers for the package will agree with the svn tag and that they always increase with newer versions! Tagging is achieved with the following command.

svn copy https://svn.cern.ch/reps/gridinfo/example/trunk https://svn.cern.ch/reps/gridinfo/example/tags/R_x_y_z -m "New Release"

Building

Packages released in the EMI 3 repositories MUST be built with the CERN koji build system. Check the How to Build packages in the Agile Project Infrastructure to get a koji account and learn all the details to use the CERN koji build system.

If a package is released for the first time, the following commands need to be executed:

koji add-pkg --owner=malandes bdii6 package-name
koji add-pkg --owner=malandes bdii6-testing package-name
koji add-pkg --owner=malandes bdii6-stable package-name
koji add-pkg --owner=malandes bdii7 package-name
koji add-pkg --owner=malandes bdii7-testing package-name
koji add-pkg --owner=malandes bdii7-stable package-name

The command to build the package in koji is:

koji build bdii6 srpm-package
koji build bdii7 srpm-package

If the build is successful the package will be available in the testing repository SL6 and SL7. In order to install packages from the testing repository, use the following repo files (Example below for SL6, please change bdii6 with bdii7 for the SL7 repo):

[bdii6-testing]
name=bdii6-testing
baseurl=http://linuxsoft.cern.ch/internal/repos/bdii6-testing/$basearch/os/
enabled=1
gpgcheck=0
priority=30 

Testing and Quality Assurance

Once the testing repository has been created, testing can begin. The testing required is outlined in the test plan. The tests described in the test plan MUST be carried out for each component before it is considered for release. The CERN Openstack infrastructure currently hosts the BDII testbed.

It has to be noted as well that all the standard coding conventions should be followed and installed software should use the directory structure as specified in the Filesystem Hierarchy Standard (link is external). Packages should also be sanity checked before being moved into the testing repository.

For integration testing with other middleware services, notify middleware developers that a new BDII update is available in the testing repository through the EMI EMT (link sends e-mail) mailing list.

For testing in production conditions, notify sites that are participating in early evaluation that a new BDII update is available in the testing repository.
Release

Packages to be released in EMI 3 that have succesfully passed all tests can be promoted to the stable repository by running:

koji tag-pkg bdii6-stable package-name-version.el6
koji tag-pkg bdii7-stable package-name-version.el7

This will create the packages also in the Linuxsoft repository.

The release should be announced and documented in the BDII releases web page. This page offers an RSS feed.

The corresponding JIRA and GGUS tickets that are fixed in the release, should be closed including a link to the release notes.

This action MUST be accompanied with a notification to the EMI EMT (link sends e-mail) mailing list and the URT (link sends e-mail)mailing list.The EMI and UMD release managers will take care of populating the relevant repositories. Note that only UMD releases are guaranteed by a succesful staged rollout (link is external).
Defect Tracking

    The main entry point for users and system administrator is GGUS (link is external).
    GGUS notification are sent to the project-grid-info-support (link sends e-mail) email list.
    Defects and enhancements are tracked using the Grid Information System Jira tracker.

EPEL

BDII releases are also released in EPEL. In order to release a package in EPEL you need to become a package maintainer. Find out more details in the following links:

    How to get your packager status (link is external)
    Join the package collection maintainers (link is external)
    How to get sponsored (link is external) into the packager group
    Package review process (link is external)

The status of EPEL releases for the BDII is sumarised in this twiki. For further details, please use the Fedora Package database (link is external).
You are here
Home


