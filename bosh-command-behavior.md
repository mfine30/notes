Assume updating an instance group called mysql with 3 instances.

Each row below describes a `Deployment Change` that was applied to an existing deployment. That change left the `Entity` in the `Current State`. The `User Action` is the type of command the user runs on the `Entity`, and the `State to Update to?` is if the user specifies "last successful manifest" or "desired manifest" when that `User Action` is run.

`Current State` can be one of `updated`, `not updated`, or `failed

Entity | Deployment Change | Current State | User Action | State to Update to? | Expected Behavior
-------|---------------|-------|-------------|--------------------|-------------------
`instance/INDEX` | Update release | Updated | stop | n/a | keep desired release on VM
`instance/INDEX` | Disk scale | Updated | stop | n/a | keep new disk attached
`instance/INDEX` | Property change | Updated | stop | n/a | updated properties stay on VM
`instance/INDEX` | Update link provider | Updated | stop | n/a | link provider provides new link
`instance/INDEX` | Update release | Failed | stop | n/a | keep desired release on VM
`instance/INDEX` | Disk scale | Failed | stop | n/a | keep new disk attached
`instance/INDEX` | Property change | Failed | stop | n/a | updated properties stay on VM
`instance/INDEX` | Update link provider | Failed | stop | n/a | link provider provides new link
`instance/INDEX` | Update release | Not Updated | stop | n/a | keep old release on VM
`instance/INDEX` | Disk scale | Not Updated | stop | n/a | keep old disk attached
`instance/INDEX` | Property change | Not Updated | stop | n/a | old properties stay on VM
`instance/INDEX` | Update link provider | Not Updated | stop | n/a | link provider provides old link
`instance/INDEX` | Update release | Updated, Failed, Not Updated | stop hard | n/a | delete VM
`instance/INDEX` | Disk scale | Updated, Failed, Not Updated | stop hard | n/a | delete VM; orphan disk
`instance/INDEX` | Property change | Updated, Failed, Not Updated | stop hard | n/a | delete VM
`instance/INDEX` | Update link provider | Updated, Failed, Not Updated | stop hard | n/a | delete VM
