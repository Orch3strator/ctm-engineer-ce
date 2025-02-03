# ctm-engineer-ce
Control-M Engineer Community Edition

## Managed File Transfer

### Inventory

### Monitoring

### Expert


## Control-M AAPI

- Using the Config service, you can access, update, and add configuration data for the major components of the Control-M environment.

- The deploy service allows you to transfer job and configuration definitions to Control-M. Once a job is deployed, it will be scheduled by Control-M according to its scheduling criteria and dependencies. The deploy overwrites any existing definition of the same name. 


## Inventory

### Servers

The config servers::get command enables you to get a list of Control-M/Server.

``` markdown title="Get all Control-M Servers"
ctm config servers::get
```

### Agents

The config server:agents::get command enables you to get a list of all Agents registered to the Control-M/Server, along with basic details about each Agent. 

``` markdown title="Get all Control-M Agents"
ctm config server:agents::get <server> ["<agent_pattern>"]
```

| Field	| Description |
| ------------- | ------------- |
| server | Name of Control-M/Server |
| agent_pattern | (Optional) Filter the list to include only agents that match a specified pattern. |


### Hostgroups

The config server:hostgroups::get command enables you to get a list of host groups defined in the Control-M/Server. 

``` markdown title="Returns a list of host groups defined in the Control-M/Server."
config server:hostgroups::get
```

| Field	| Description |
| ------------- | ------------- |
| server | Name of Control-M/Server |


The config server:hostgroup:agents::get command enables you to get the list of Agents in a host group, provided that you are authorized to manage this host group. 

``` markdown title="Returns a list of agents of a host group (provided that you are authorized to manage this host group)"
config server:hostgroup:agents::get
```

| Field	| Description |
| ------------- | ------------- |
| server | Name of Control-M/Server |
| hostgroup | Name of host group |

### Connection Profiles

The deploy connectionprofiles:centralized::get command enables you to get the full definitions of centralized connection profiles, based on specified search criteria.

``` markdown title="Get centralized deployed connection profile"
ctm deploy connectionprofiles:centralized::get -s <search query>
```

| Field	| Description |
| ------------- | ------------- |
| type | Type of connection profile |
| name | Name of connection profile(s). |

Filter applied: type=FileTransfer

The deploy connectionprofiles:local::get command enables you to get the details of local connection profiles associated with your Control-M/Agents, based on specified search criteria.

``` markdown title="Returns the details of local connection profiles associated with your Control-M/Agents, based on specified search criteria."
ctm deploy connectionprofiles:local::get -s <search query>
```

| Field	| Description |
| ------------- | ------------- |
| server | Name of Control-M/Server |
| agent | Name of Control-M/Agent |
| type | Type of connection profile |


Filter applied: type=FileTransfer


## Monitoring

The config server:agent::pingcommand enables you to check if the Agent is available.

``` markdown title="Checks if the Control-M/Agent is available."
ctm config server:agent::ping <server> <agent> [-f <configuration file>]
```

| Field	| Description |
| ------------- | ------------- |
| server | Name of Control-M/Server |
| agent | Name of Control-M/Agent |
| configuration file | (Optional) JSON file that contains additional parameters. |


The deploy connectionprofile:centralized::test command enables you to test an existing centralized connection profile on a specific Control-M/Agent.

``` markdown title="The deploy connectionprofile:centralized::test command enables you to test an existing centralized connection profile on a specific Control-M/Agent."
ctm deploy connectionprofile:centralized::test <type> <name> <server> <agent>
```

| Field	| Description |
| ------------- | ------------- |
| server | Name of Control-M/Server |
| agent | Name of Control-M/Agent |
| type | Determines the connection profile type. |
| name | Defines the connection profile name.  |

Filter applied: type=FileTransfer




