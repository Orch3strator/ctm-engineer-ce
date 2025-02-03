# ctm-engineer-ce
Control-M Engineer Community Edition

## Managed File Transfer

### Configuration

The CTM Engineer is driven by the command arguments and a config file located:
- Windows: C:\ProgramData\engineer\configs
- Linux: /home/${USER}/.config/engineer/configs/engineer.json

Example: [engineer.json](example/engineer.json)

#### Requirements

- Python 3.1x
- Control-M Automation API token
- Network access to Control-M Enterprise Manager

### Inventory

Get an inventory of your Control-M resources, focused on Managed File Transfer.

A report is svaed to:
- C:\ProgramData\engineer\data\ctm-inventory.json
- /home/${USER}/.config/engineer/data/ctm-inventory.json


``` markdown title="Linux"
engineer -i
```

``` markdown title="Windows"
engineer.exe -i
```

### Monitoring

Get the agent and CCP status of your Control-M Servers, focused on Managed File Transfer.

- Get List of Control-M Servers
- For each Server, get:
    - Agents
    - CCP
- Ping each Agent
- Test CCP with live Agent

A report is svaed to:
- C:\ProgramData\engineer\data\ctm-monitoring.json
- /home/${USER}/.config/engineer/data/ctm-monitoring.json


``` markdown title="Linux"
engineer -m
```

``` markdown title="Windows"
engineer.exe -m
```

### Help

A log file is written to: 
- C:\ProgramData\engineer\logs\engineer.log
- /home/${USER}/.config/engineer/logs/engineer.log

``` markdown title="Linux"
engineer -h
```

``` markdown title="Windows"
engineer.exe -h
```

### Expert

The expert mode combines "monitoring" and "Folders".

A report is svaed to:
- C:\ProgramData\engineer\data\<filter-name>ctm-expert.json
- /home/${USER}/.config/engineer/data/<filter-name>ctm-expert.json

``` markdown title="Linux"
engineer -e -f <filter-name>
```

``` markdown title="Windows"
engineer.exe -e -f <filter-name>
```


## Control-M AAPI

- Using the Config service, you can access, update, and add configuration data for the major components of the Control-M environment.

- The deploy service allows you to transfer job and configuration definitions to Control-M. Once a job is deployed, it will be scheduled by Control-M according to its scheduling criteria and dependencies. The deploy overwrites any existing definition of the same name. 

### Deploy Service

The deploy service allows you to transfer job and configuration definitions to Control-M. 

### Config Service

The config service allows you to configure the Control-M environment.

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




