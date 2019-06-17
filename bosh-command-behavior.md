Assume updating an instance group called mysql with 3 instances.

This section describes how BOSH should behave

Entity | Deploy Change | State | User Action | Current or Desired | Expected Behavior
-------|---------------|-------|-------------|--------------------|-------------------
`instance/INDEX` | Update release | Failed | stop | desired | keep desired release on VM
`instance/INDEX` | Disk scale | Failed | stop | desired | new disk stays attached
`instance/INDEX` | Property change | Failed | stop | desired | updated properties stay on VM
`instance/INDEX` | Update link provider | Failed | stop | desired | link provider provides new link
