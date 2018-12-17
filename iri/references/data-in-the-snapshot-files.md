# Data in the snapshot files

When the IRI creates a local snapshot, the following files are created in the path of the [`LOCAL_SNAPSHOTS_BASE_PATH`] configuration parameter:
* snapshot.meta
* snapshot.state

The snapshot.state file contains a list of all addresses that have a balance greater than 0 in an IOTA network. This data is displayed in the following format:
```
address;balance
```

This table contains the data that is added to the snapshot.meta file during a [local snapshot](/iri/concepts/local-snapshot.md):

| **Data**|    **Description** |                                      
| :-----: |  :---------------: | 
|Milestone hash |The hash of the milestone transaction that the IRI uses as a starting point to build its ledger|
|Milestone index | The index of the milestone transaction that the IRI uses as a starting point to build its ledger |
|Unix timestamp |The time that the snapshot files were created |
|Total number of solid entry points|Solid entry points are the confirmed transactions for which the IRI had all of their approvers in its ledger during the time of the snapshot|
|Total number of seen milestones |This number is the same as the [`LOCAL_SNAPSHOTS_DEPTH` configuration parameter](/iri/references/iri-configuration-options.md#local-snapshots-depth) |
|List of solid entry points | A semicolon-separated list of transaction hashes of solid entry points and the milestone index that made them solid|
|List of seen milestones | A semicolon-separated list of milestone transaction hashes that the IRI starts from when synchronzing its ledger with its neighbor IRI nodes |