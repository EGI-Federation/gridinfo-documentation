.. _test_plan:

Test Plan
=========

Philosophy
----------

The Grid Infrastructure is composed of many Grid Services that work together to
provide users with the resources they need to achieve their goals. As such, the
Grid is "service-centric" and hence the service is the focus of the process.
This concept fits well with The Information Technology Infrastructure Library
(ITIL) practices for managing Information Technology services. In particular
the Service Support discipline can be leveraged, which addresses Incident
Management, Problem Management, Change Management, Release Management and
Configuration Management.

Grid Services are able to work together in the infrastructure as they implement
well defined interface specifications (eg. HTTP for the web). Failure to
strictly adhere to these specifications will break the infrastructure and such
these interfaces must be fixed and owned by an oversight body for the
infrastructure (eg. W3C). A Grid Service must always adhere to these
specifications and a service update must not break or diverge from the
specification. If a new specification is required, this must be endorsed by the
oversight body for that infrastructure and implemented in a way that is
backwards compatible. This typically requires services to support two versions
during the migration period (eg. IPV4 to IPV6 transition).

As Grid Services are linked by the interface specification alone, services may
be provided by multiple vendors as long as each has faithfully implemented the
interface specification. Multiple versions of a service should be able to
coexist in the infrastructure. The only exception is after a specification
migration when the old version becomes obsolete.

It must be pointed out a service can be simple, a daemon process running on a
single machine, or complex, hundreds of machines running different clustered
sub services such as databases and web servers. The user is typically hidden
from the implementation details and only experiences the service provided via
the interface, however, the Service Provider does care about the implementation
details of the service. In the case of a complex service, the components of
that service may be provided by many different vendors and in the scenario
where sub services are used, these are also linked by interface specifications.
The suggest that where as the infrastructure is integrated at the service
level, services are are integrated at the sub service level or component level.

It must also be noted that developing stand-alone program and running an
on-line service are two very different things. Instead of releasing a new
version of a program every couple of years, on-line services live in a
perpetual cycle of product improvement and instantaneous user feedback. As
such, service development typically takes a roll-forward approach where the
instance of the service should always be running the latest version and fixes
are provided in a newer version, rather than applying the fixes to a branch of
an old version.

Testing Strategy
----------------

The focus of the strategy is the concept of a service update. A service is a
collection of stand-alone software components that work together to provide the
service. A service update is a sub-set of these components which have a newer
version than what already exists for the service.  This naturally divides the
process of providing a service update into the update itself and providing an
update to the component. As a component may be used in many other places other
than the service, these to processes should be view as decoupled from each
other. Development represents the area of producing the component and
Integration is the process of creating a service update from a collection of
components. During Development, developers are responsible for the quality of
the components which they maintain. As they know the component in detail, they
should also understand how best to test the component. Each component should
contain tests that can be run in developer mode ie. directly from the VCS. The
implementation of this is the choice of the developer, however, the testing
method must be documented. Before a release tag is made for the component, the
developer must run the tests and ensure they all pass.  The focus of this level
of testing is to verify all the supported functionally of the component. The
process of Integration starts when all the components are available and ends
with the provision of a service update. It is the responsibility of the
integrator to ensure that the service update is of high quality. In order to
achieve this goal a multi-level testing strategy will be employed.

Level 0: Component
``````````````````

**Aim**: To verify the main functionality

Each component should be accompanied by a set of tests that verifies the basic
functionality of that component. These tests should be included in the same
source repository and be able to run both during development and final
deployment. The tests should be run by the developer before the component is
tagged and hence the developer is responsible for developing these tests. A
test for the new functionally or software bugs should be created before
development work commences.

Level 1: Service Ping
`````````````````````

**Aim**: To verify that the service up.

The result of the integration phase is a set of deployable packages along with
configuration methods. After an instance has been installed and configured, it
must be verified that the service is working. Typically a service is up or down
and hence a simple service 'ping' test should suffice. The tests are required
during day to day operations to ensure that the service is up and hence can be
reused for this purpose.

Level 2: Service Functionality
``````````````````````````````

**Aim**: To verify the full functionality of the service.

After a service has been installed and it is up, functionality tests can be
carried out to ensure that all the supported functionality is working. If
possible, this can be achieve by re-running the component tests. However,
additional tests will be required if this is not possible or the component
tests do not cover functionality provided by the integrated service.

Level 3: Service Performance and Stress Testing
```````````````````````````````````````````````

**Aim**: To verify the performance of the service.

A benchmarking test is required to measure the performance of the service. This
should be run to ensure that each new release does not degraded the
performance. In additional, how the performance changes over time must be
measured.

Level 4: Infrastructure
```````````````````````

**Aim**: To verify the full system work-flow.

Full end-to-end Grid work flows need to be tested. This will include verifying
that different versions of the Services work together. This will be achieved
via the use of a staged roll out process.
