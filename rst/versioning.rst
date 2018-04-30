.. _versioning:

Versioning
==========

SEMVER
------
We follow `SEMVER <http://semver.org/>`_ standards, using a MAJOR.MINOR.PATCH versioning scheme. This means that we will increment versioning in the following way:

* MAJOR version when we make incompatible API changes
* MINOR version when we add functionality in a backwards-compatible manner
* PATCH version when we make backwards-compatible bug fixes

There are two seperate version numbers that users should be aware of. One for the API service, and one for the data returned by the API. Versioning is seperated in this way because changes to the service may be rolled out that do not affect the PUBG API data. The version of the API service is available in the data returned by the /status endpoint. The data version can be found in the changelog.



Deprecation Policy
------------------
Deprecated fields and data will be announced at least one week in advance in the "Upcoming Changes" section at the top of the changelog. Once deprecated, the field/data will typically be hardcoded to zero for 14 days until the data retention period has turned over before being removed entirely.
