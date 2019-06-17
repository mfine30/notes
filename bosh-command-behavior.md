Assume updating an instance group called mysql with 3 instances.

Each row below describes a `Deployment Change` that was applied to an existing deployment. That change left the `Entity` in the `Current State`. The `User Action` is the type of command the user runs on the `Entity`, and the `State to Update to?` is if the user specifies "last successful manifest" or "desired manifest" when that `User Action` is run.

`Current State` can be one of `updated`, `not updated`, or `failed

Entity | Deployment Change | Current State | User Action | State to Update to? | Expected Behavior
-------|---------------|-------|-------------|--------------------|-------------------
`instance/INDEX` | Update release | Updated | stop | new manifest | keep desired release on VM
`instance/INDEX` | Disk scale | Updated | stop | new manifest | keep new disk attached
`instance/INDEX` | Property change | Updated | stop | new manifest | updated properties stay on VM
`instance/INDEX` | Update link provider | Updated | stop | new manifest | link provider provides new link
`instance/INDEX` | Update release | Failed | stop | new manifest | keep desired release on VM
`instance/INDEX` | Disk scale | Failed | stop | new manifest | keep new disk attached
`instance/INDEX` | Property change | Failed | stop | new manifest | updated properties stay on VM
`instance/INDEX` | Update link provider | Failed | stop | new manifest | link provider provides new link
`instance/INDEX` | Update release | Not Updated | stop | new manifest | Error; require user to do normal deploy
`instance/INDEX` | Disk scale | Not Updated | stop | new manifest | Error; require user to do normal deploy
`instance/INDEX` | Property change | Not Updated | stop | new manifest | Error; require user to do normal deploy
`instance/INDEX` | Update link provider | Not Updated | stop | new manifest | Error; require user to do normal deploy
`instance/INDEX` | Update release | Updated | stop hard | new or old manifest | delete VM
`instance/INDEX` | Disk scale | Updated | stop hard | new or old manifest | delete VM; orphan disk
`instance/INDEX` | Property change | Updated | stop hard | new or old manifest | delete VM
`instance/INDEX` | Update link provider | Updated | stop hard | new or old manifest | delete VM
