# Changelog

Patch release for MSR 4.13.4 that includes the following changes.

* [MSRH-553] Added a null check to the Redis password helper template to prevent
   Helm installation failures when the referenced secret does not exist.
* [FIELD-7983] Fixed an issue wherein creation of replication rules with filters
   through Swagger failed with an invalid JSON error.
