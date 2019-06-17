Assume updating an instance group called mysql with 3 instances.

Each row below describes a `Deployment Change` that was applied to an existing deployment. That change left the `Entity` in the `Current State`. The `User Action` is the type of command the user runs on the `Entity`, and the `State to Update to?` is if the user specifies "last successful manifest" or "desired manifest" when that `User Action` is run.

`Current State` can be one of `updated`, `not updated`, or `failed

Entity | Deployment Change | Current State | User Action | State to Update to? | Expected Behavior
-------|---------------|-------|-------------|--------------------|-------------------
`instance/INDEX` | Update release | Failed | stop | new manifest | keep desired release on VM
`instance/INDEX` | Disk scale | Failed | stop | new manifest | new disk stays attached
`instance/INDEX` | Property change | Failed | stop | new manifest | updated properties stay on VM
`instance/INDEX` | Update link provider | Failed | stop | new manifest | link provider provides new link
