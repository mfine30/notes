## Documentation for New Commands 

We will eventually create proper CLI commands for these endpoints, 
either by replacing the existing `bosh start` and `bosh stop` type commands,
or creating entirely new commands. In the interim, they can be run with new endpoints on a BOSH Director [v270.3.0 or later](https://github.com/cloudfoundry/bosh/releases/tag/v270.3.0).

At a high level, the new endpoints follow the structure
`/deployments/:deployment/instance_groups/:instance_group/:id/actions/:action`. 
  * `:deployment` is a deployment name
  * `:instance_group` is an instance group within the deployment
  * `:id` is an instance UUID or index
  * `:action` is the action to perform such as `start` or `stop`

Command behavior should follow information defined [in this document](https://github.com/mfine30/notes/blob/master/bosh-command-behavior.md)

### Using New Endpoints/Commands
* [Stop](#stop)
* [Start](#start)
* [Recreate](#recreate)
* [Restart](#restart)
* [View Task Output](#view-task-output)

## Stop

### Stop

To stop a specific instance
```
$ bosh curl -X POST /deployment/dep1/instance_group/ig1/4/actions/stop

{"id":4790,"state":"processing","description":"stop instance","timestamp":1560897492,"started_at":null,"result":null,"user":"admin","deployment":"lifecycle","context_id":""}
```

#### Skip Drain

To stop a specific instance and delete its associated VM
(i.e. `bosh stop --hard`) append `?skip-drain=true` to the end of the endpoint
```
$ bosh curl -X POST /deployment/dep1/instance_group/ig1/4/actions/stop?skip_drain=true`
```

### Stop Instance and Delete VM

To stop a specific instance and delete its associated VM
(i.e. `bosh stop --hard`) append `?hard=true` to the end of the endpoint
```
$ bosh curl -X POST /deployment/dep1/instance_group/ig1/4/actions/stop?hard=true`
```

## Start
To start a specific instance

```
$ bosh curl -X POST /deployments/dep2/instance_groups/:instance_group/:index/actions/start

{"id":4790,"state":"processing","description":"stop instance","timestamp":1560897492,"started_at":null,"result":null,"user":"admin","deployment":"lifecycle","context_id":""}
```

## Recreate
To recreate a specific instance (as of BOSH v270.4.0)

```
$ bosh curl -X POST /deployments/dep2/instance_groups/:instance_group/:index/actions/recreate

{"id":4790,"state":"processing","description":"recreate instance","timestamp":1560897492,"started_at":null,"result":null,"user":"admin","deployment":"lifecycle","context_id":""}
```

## Restart
To restart a specific instance (as of BOSH v270.4.0)

```
$ bosh curl -X POST /deployments/dep2/instance_groups/:instance_group/:index/actions/restart

{"id":4790,"state":"processing","description":"restart instance","timestamp":1560897492,"started_at":null,"result":null,"user":"admin","deployment":"lifecycle","context_id":""}
```

## View Task Output 
Each of the commands above will trigger an underlying BOSH task. To view the output of that task, follow these instructions.

1. Run the `bosh curl` command to stop/start an instance
1. Retrieve the value of `"id"` – the task ID – from the curl's JSON response
1. `bosh task XXX`
