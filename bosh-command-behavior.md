## Table of Contents
- [Intro](#intro)
- [Commands on a Specific Instance](#commands-on-a-specific-instance)
  * [Stop Behavior](#stop-behavior)
  * [Start Behavior](#start-behavior)
- [Commands on Instance Group](#commands-on-an-instance-group)
  * [Stop Behavior](#stop-behavior-1)
  * [Start Behavior](#start-behavior-1)

### Intro

This document describes the intended behavior of BOSH when an operator runs a command against an instance, instance group, or deployment and that "entity" is in a given state.

Each row below describes a `Deployment Change` that was applied to an existing deployment. That change left the `Entity` in the `Current State`. The `User Action` is the type of command the user runs on the `Entity`, and the `State to Update to?` is if the user specifies "last successful manifest" or "desired manifest" when that `User Action` is run.

### Commands on a Specific Instance

#### Stop Behavior

Entity | Deployment Change | Current Instance State | User Action | Which Manifest To Use? | Expected Behavior
-------|---------------|-------|-------------|--------------------|-------------------
`instance/INDEX` | Update release | Updated | stop | n/a | keep new manifest release on VM
`instance/INDEX` | Disk scale | Updated | stop | n/a | keep new manifest disk attached
`instance/INDEX` | Property change | Updated | stop | n/a | keep new manifest properties on VM
`instance/INDEX` | Update link provider | Updated | stop | n/a | provide new manifest link
`instance/INDEX` | Trusted Certs | Updated | stop | n/a | include new trusted certs
`instance/INDEX` | Unmanaged Disks | Updated | stop | n/a | keep new manifest disks available
`instance/INDEX` | Update release | Failed | stop | n/a | keep new manifest release on VM
`instance/INDEX` | Disk scale | Failed | stop | n/a | keep new manifest disk attached
`instance/INDEX` | Property change | Failed | stop | n/a | keep new manifest properties on VM
`instance/INDEX` | Update link provider | Failed | stop | n/a | provide new manifest link
`instance/INDEX` | Trusted Certs | Failed | stop | n/a | include new trusted certs
`instance/INDEX` | Unmanaged Disks | Failed | stop | n/a | keep new manifest disks available
`instance/INDEX` | Update release | Not Updated | stop | n/a | keep last successful manifest release on VM
`instance/INDEX` | Disk scale | Not Updated | stop | n/a | keep last successful manifest disk attached
`instance/INDEX` | Property change | Not Updated | stop | n/a | keep last successful manifest properties on VM
`instance/INDEX` | Update link provider | Not Updated | stop | n/a | provides last successful manifest link
`instance/INDEX` | Trusted Certs | Not Updated | stop | n/a | include last successful trusted certs
`instance/INDEX` | Unmanaged Disks | Not Updated | stop | n/a | keep last successful disks available
`instance/INDEX` | Update release | Updated, Failed, Not Updated | stop hard | n/a | delete VM
`instance/INDEX` | Disk scale | Updated, Failed, Not Updated | stop hard | n/a | delete VM; keep disk associated with instance
`instance/INDEX` | Property change | Updated, Failed, Not Updated | stop hard | n/a | delete VM
`instance/INDEX` | Update link provider | Updated, Failed, Not Updated | stop hard | n/a | delete VM
`instance/INDEX` | Trusted Certs | Updated, Failed, Not Updated | stop hard | n/a | delete VM
`instance/INDEX` | Unmanaged Disks | Updated, Failed, Not Updated | stop hard | n/a | delete VM; keep disks associated with instance

#### Start Behavior

Entity | Deployment Change | Current Instance State | User Action | Which Manifest To Use? | Expected Behavior
-------|---------------|-------|-------------|--------------------|-------------------
`instance/INDEX` | Update release | Updated | start | new manifest | keep new manifest release on VM
`instance/INDEX` | Disk scale | Updated | start | new manifest | keep new manifest disk attached
`instance/INDEX` | Property change | Updated | start | new manifest | keep new manifest properties on VM
`instance/INDEX` | Update link provider | Updated | start | new manifest | provide new manifest link
`instance/INDEX` | Trusted Certs | Updated | start | new manifest | keep new trusted certs on VM
`instance/INDEX` | Unmanaged Disks | Updated | start | new manifest | keep new manifest disks attached
`instance/INDEX` | Update release | Failed | start | new manifest | keep new manifest release on VM
`instance/INDEX` | Disk scale | Failed | start | new manifest | keep new manifest disk attached
`instance/INDEX` | Property change | Failed | start | new manifest | keep new manifest properties on VM
`instance/INDEX` | Update link provider | Failed | start | new manifest | provide new manifest link
`instance/INDEX` | Trusted Certs | Failed | start | new manifest | keep new trusted certs on VM
`instance/INDEX` | Unmanaged Disks | Failed | start | new manifest | keep new manifest disks attached
`instance/INDEX` | Update release | Not Updated | start | new manifest | error; require deploy to update 
`instance/INDEX` | Disk scale | Not Updated | start | new manifest | error; require deploy to update 
`instance/INDEX` | Property change | Not Updated | start | new manifest | error; require deploy to update 
`instance/INDEX` | Update link provider | Not Updated | start | new manifest | error; require deploy to update
`instance/INDEX` | Trusted Certs | Not Updated | start | new manifest | error; require deploy to update
`instance/INDEX` | Unmanaged Disks | Not Updated | start | new manifest | error; require deploy to update
`instance/INDEX` | Update release | Updated | start | last successful | last successful manifest release on VM
`instance/INDEX` | Disk scale | Updated | start | last successful | migrate disk contents to last successful manifest disk state
`instance/INDEX` | Property change | Updated | start | last successful | last successful manifest properties on VM
`instance/INDEX` | Update link provider | Updated | start | last successful | provide last successful manifest link
`instance/INDEX` | Trusted Certs | Updated | start | last successful | **keep new trusted certs on VM**
`instance/INDEX` | Unmanaged Disks | Updated | start | last successful | make last successful manifest disk types available
`instance/INDEX` | Update release | Failed | start | last successful | last successful manifest release on VM
`instance/INDEX` | Disk scale | Failed | start | last successful | migrate disk contents to last successful manifest disk state
`instance/INDEX` | Property change | Failed | start | last successful | last successful manifest properties on VM
`instance/INDEX` | Update link provider | Failed | start | last successful | provide last successful manifest link
`instance/INDEX` | Trusted Certs | Failed | start | last successful | **keep new trusted certs on VM**
`instance/INDEX` | Unmanaged Disks | Failed | start | last successful | make last successful manifest disk types available
`instance/INDEX` | Update release | Not Updated | start | last successful | already in correct state; just start
`instance/INDEX` | Disk scale | Not Updated | start | last successful | already in correct state; just start
`instance/INDEX` | Property change | Not Updated | start | last successful | already in correct state; just start
`instance/INDEX` | Update link provider | Not Updated | start | last successful | already in correct state; just start
`instance/INDEX` | Trusted Certs | Not Updated | start | last successful | already in correct state; just start
`instance/INDEX` | Unmanaged Disks | Not Updated | start | n/a | already in correct state; just start

### Commands on an Instance Group

#### Stop Behavior

Entity | Deployment Change | Current Instance State | User Action | Which Manifest To Use? | Expected Behavior
-------|---------------|-------|-------------|--------------------|-------------------
`instance_group` | Update release | Updated | stop | n/a | keep new manifest release on VMs
`instance_group` | Disk scale | Updated | stop | n/a | keep new manifest disks attached
`instance_group` | Property change | Updated | stop | n/a | keep new manifest properties on VMs
`instance_group` | Update link provider | Updated | stop | n/a | provide new manifest links
`instance_group` | Trusted Certs | Updated | stop | n/a | include new trusted certs
`instance_group` | Unmanaged Disks | Updated | stop | n/a | keep new manifest disks available
`instance_group` | Update release | Failed | stop | n/a | keep all VMs in current
`instance_group` | Disk scale | Failed | stop | n/a | keep all disks in current attachment
`instance_group` | Property change | Failed | stop | n/a | keep all VMs in current state
`instance_group` | Update link provider | Failed | stop | n/a | each instance provides current link
`instance_group` | Trusted Certs | Failed | stop | n/a | each instance includes current certs
`instance_group` | Unmanaged Disks | Failed | stop | n/a | keep currently attached disks
`instance_group` | Update release | Not Updated | stop | n/a | keep last successful manifest release on VMs
`instance_group` | Disk scale | Not Updated | stop | n/a | keep last successful manifest disks attached
`instance_group` | Property change | Not Updated | stop | n/a | keep last successful manifest properties on VMs
`instance_group` | Update link provider | Not Updated | stop | n/a | provides last successful manifest links
`instance_group` | Trusted Certs | Not Updated | stop | n/a | include last successful trusted certs
`instance_group` | Unmanaged Disks | Not Updated | stop | n/a | keep last successful disks available
`instance_group` | Update release | Updated, Failed, Not Updated | stop hard | n/a | delete VMs
`instance_group` | Disk scale | Updated, Failed, Not Updated | stop hard | n/a | delete VMs; keep disks associated with instances
`instance_group` | Property change | Updated, Failed, Not Updated | stop hard | n/a | delete VMs
`instance_group` | Update link provider | Updated, Failed, Not Updated | stop hard | n/a | delete VMs
`instance_group` | Trusted Certs | Updated, Failed, Not Updated | stop hard | n/a | delete VMs
`instance_group` | Unmanaged Disks | Updated, Failed, Not Updated | stop hard | n/a | delete VMs; keep disks associated with instances


#### Start Behavior

Entity | Deployment Change | Current Instance State | User Action | Which Manifest To Use? | Expected Behavior
-------|---------------|-------|-------------|--------------------|-------------------
`instance_group` | Update release | Updated | start | new manifest | keep new manifest release on VMs
`instance_group` | Disk scale | Updated | start | new manifest | keep new manifest disks attached
`instance_group` | Property change | Updated | start | new manifest | keep new manifest properties on VMs
`instance_group` | Update link provider | Updated | start | new manifest | provide new manifest links
`instance_group` | Trusted Certs | Updated | start | new manifest | keep new trusted certs on VM
`instance_group` | Unmanaged Disks | Updated | start | new manifest | keep new manifest disks attached
`instance_group` | Update release | Failed | start | new manifest | keep new manifest release on all VMs
`instance_group` | Disk scale | Failed | start | new manifest | keep new manifest disk attached on all VMs
`instance_group` | Property change | Failed | start | new manifest | keep new manifest properties on all VMs
`instance_group` | Update link provider | Failed | start | new manifest | provide new manifest links
`instance_group` | Trusted Certs | Failed | start | new manifest | keep new trusted certs on all VMs
`instance_group` | Unmanaged Disks | Failed | start | new manifest | keep new manifest disks attached on all VMs
`instance_group` | Update release | Not Updated | start | new manifest | error; require deploy to update 
`instance_group` | Disk scale | Not Updated | start | new manifest | error; require deploy to update 
`instance_group` | Property change | Not Updated | start | new manifest | error; require deploy to update 
`instance_group` | Update link provider | Not Updated | start | new manifest | error; require deploy to update
`instance_group` | Trusted Certs | Not Updated | start | new manifest | error; require deploy to update
`instance_group` | Unmanaged Disks | Not Updated | start | new manifest | error; require deploy to update
`instance_group` | Update release | Updated | start | last successful | last successful manifest release on VMs
`instance_group` | Disk scale | Updated | start | last successful | migrate disk contents to last successful manifest disk state
`instance_group` | Property change | Updated | start | last successful | last successful manifest properties on VMs
`instance_group` | Update link provider | Updated | start | last successful | provide last successful manifest links
`instance_group` | Trusted Certs | Updated | start | last successful | **keep new trusted certs on VM**
`instance_group` | Unmanaged Disks | Updated | start | last successful | make last successful manifest disk types available
`instance_group` | Update release | Failed | start | last successful | last successful manifest release on VMs
`instance_group` | Disk scale | Failed | start | last successful | migrate disk contents to last successful manifest disk state
`instance_group` | Property change | Failed | start | last successful | last successful manifest properties on VMs
`instance_group` | Update link provider | Failed | start | last successful | provide last successful manifest link
`instance_group` | Trusted Certs | Failed | start | last successful | **keep new trusted certs on VM**
`instance_group` | Unmanaged Disks | Failed | start | last successful | make last successful manifest disk types available
`instance_group` | Update release | Not Updated | start | last successful | already in correct state; just start
`instance_group` | Disk scale | Not Updated | start | last successful | already in correct state; just start
`instance_group` | Property change | Not Updated | start | last successful | already in correct state; just start
`instance_group` | Update link provider | Not Updated | start | last successful | already in correct state; just start
`instance_group` | Trusted Certs | Not Updated | start | last successful | already in correct state; just start
`instance_group` | Unmanaged Disks | Not Updated | start | n/a | already in correct state; just start
