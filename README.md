# ctm-engineer-ce
Control-M Engineer Community Edition

## Managed File Transfer

### Inventory

### Monitoring

### Expert


## Control-M AAPI

- Using the Config service, you can access, update, and add configuration data for the major components of the Control-M environment.

- The deploy service allows you to transfer job and configuration definitions to Control-M. Once a job is deployed, it will be scheduled by Control-M according to its scheduling criteria and dependencies. The deploy overwrites any existing definition of the same name. 


### Servers

``` markdown title="Get all Control-M Servers"
ctm config servers::get
```

### Agents

``` markdown title="Get all Control-M Agents"
ctm config server:agents::get <server> ["<agent_pattern>"]
```

| Field	| Description |
| ------------- | ------------- |
| server | Name of Control-M/Server |
| agent_pattern | (Optional) Filter the list to include only agents that match a specified pattern. |


``` markdown title="Checks if the Control-M/Agent is available."
ctm config server:agent::ping <server> <agent> [-f <configuration file>]
```

| Field	| Description |
| ------------- | ------------- |
| server | Name of Control-M/Server |
| agent | Name of Control-M/Agent |
| configuration file | (Optional) JSON file that contains additional parameters. |


### Connection Profiles


``` markdown title="Get centralized deployed connection profile"
ctm deploy connectionprofiles:centralized::get -s <search query>
```

| Field	| Description |
| ------------- | ------------- |
| type | Type of connection profile |
| name | Name of connection profile(s). |

Filter applied: type=FileTransfer


``` markdown title="Returns the details of local connection profiles associated with your Control-M/Agents, based on specified search criteria."
ctm deploy connectionprofiles:local::get -s <search query>
```

| Field	| Description |
| ------------- | ------------- |
| server | Name of Control-M/Server |
| agent | Name of Control-M/Agent |
| type | Type of connection profile |


Filter applied: type=FileTransfer

