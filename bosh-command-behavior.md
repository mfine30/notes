Assume updating an instance group called mysql with 3 instances.

This section describes how BOSH should behave

Entity | Deploy Change | State | User Action | Expected Behavior
-------|---------------|-------|-------------|------------------
`instance/INDEX` | Update release | Failed | stop in desired state | * `monit stop` jobs <br> * keep VM in current state
`instance/INDEX` | Disk scale | Failed | stop in desired state | `monit stop` jobs
`instance/INDEX` | Property change | Failed | stop | `monit stop` jobs
