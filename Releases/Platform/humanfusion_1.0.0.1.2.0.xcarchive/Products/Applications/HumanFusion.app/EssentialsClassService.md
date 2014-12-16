Sync
====

The goal of sync is to make client databases eventually consistent with all changes that occur on the server.

The Essentials template sync mechanism is as follows.

Sync Triggers
-------------

- Display of the Essentials Discover screen. This is rate limited to N sync attempt every M minutes. Both N and M are configurable.
- User initiated pull-to-refresh
- TBD: Push notification

Sync UI Design
--------------

Sync has very little interaction with or impact on the UI. The following UI events occur as a direct result of sync:

1. User initiated pull-to-refresh will show the OS standard refresh control. This control will persist until the termination of that sync process.
2. The status bar shows an activity indicator during network requests.
3. The discover screen content is updated on a per block basis. As each block is successfully processed, the discover screen will attempt to update the content displayed.

There are no other UI changes triggered as part of sync. 

Sync Modes
==========

Summary versions of Essentials classes will be synced in one of three modes:

1. Initial sync
2. Subsequent sync
3. Single-shot sync
4. Single-shot delete
5. Mark-and-sweep asset garbage collection

Initial Sync
------------

Initial sync attempts to retrieve iteratively, all Essentials summary records in blocks. It does this by starting at the current local device time and working backwards based on release date.

Initial sync is used when either:

* No summary entities are currently stored in the database.

Initial sync is triggered automatically when:

* A subsequent sync has finished processing, without regard to the success of that attempt.


Subsequent Sync
---------------

Subsequent sync is used when:

* One or more summary entities are current stored in the database.



Single-shot Sync
----------------

Single-shot sync is triggered when:

* A result block of size N from either initial or subsequent sync contains N identical releaseDate or updatedAt values. updatedAt is used for comparison in initial syncs and releaseDate is used for comparison in subsequent syncs.



Failure Modes
=============


Configuration
=============

