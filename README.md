# CTM Engineer

Control-M Engineer - Control-M Pre-Execution Validation Tool

## Overview

This project ensures that all required resources for scheduled Control-M workflows (folders) are available one hour before execution. 
It provides inventory checks, workflow validation, and monitoring to help the operations team proactively address potential issues before the actual run.


### Key Features

✅ Inventory Management – Retrieve and review Control-M folders, workflows, and their dependencies.

✅ Folder Inventory – Get a folder's **Managed File Transfer** job dependencies.

✅ Agent Availability Check – Ensure that Control-M agents executing the workflows are up and running.

✅ Basic Monitoring – Track workflow dependencies and status.

✅ Expert Mode – Provides deep monitoring, validating server, connections, agents, and workflow dependencies in a single execution.

### Use Case

- A business user schedules a folder/workflow for execution at a specific time.
- This project pre-checks all required resources (agents, connections, workflows) one hour before the scheduled execution.
- The operations team is notified if any critical resources are unavailable.
- Ensures a smooth, error-free execution when the workflow runs.

### Why This Project?

🔹 Prevents workflow failures due to missing resources.

🔹 Reduces operational downtime with proactive monitoring.

🔹 Enhances reliability of Control-M job executions.

# Installation & Configuration

### Download & Release

🚀 Latest Release: [engineer.zip](release/engineer.zip)



### Configuration

📌 The CTM Engineer is driven by the command arguments and a config file located:

- Windows: C:\ProgramData\engineer\configs
- Linux: /home/${USER}/.config/engineer/configs/engineer.json

📂 Example: [engineer.json](example/engineer.json)

#### Requirements

- Control-M Automation API token
- Network access to Control-M Enterprise Manager

📌 Only for full-access repo, not in Community Edition

- Python 3.1x


#### Build and Package

📌 Only part of full-access repo, not in Community Edition

``` markdown title="Linux"
pyinstaller --clean engineer.lin.spec --noconfirm
```

``` markdown title="Windows"
pyinstaller --clean engineer.win.spec --noconfirm
```

## Usage & Commands

### Inventory Function

📌 Get an inventory of your Control-M resources, focused on Managed File Transfer.


👉 Output is saved to:

- C:\ProgramData\engineer\data\ctm-inventory.json
- /home/${USER}/.config/engineer/data/ctm-inventory.json


``` markdown title="Linux"
engineer -i
```
``` markdown title="Linux"
engineer --inventory
```

### Folders Function

📌 Get an inventory of your Control-M Folders, focused on Managed File Transfer.

👉 Output is saved to:

- C:\ProgramData\engineer\data\ctm-folders.json
- /home/${USER}/.config/engineer/data/ctm-folders.json


``` markdown title="Linux"
engineer -f
```
``` markdown title="Linux"
engineer --folders
```

#### Output

📂 Example: [ctm-folders.json](example/ctm-folders.json)

#### Filter

The filter being applied is based on the engineer.json config file

📂 Example: [engineer.json](example/engineer.json)

``` markdown title="Filters"
"FILTERS": {
        "types": [
            {
                "type": "folders",
                "name": "ZZM",
                "folder": "ZZM_UC_MULTI*",
                "server": "ctm-lin-srv",
                "agentMode": "hostgroups"
            },
            {
                "type": "folders",
                "name": "PRIVACY_GUARD",
                "folder": "ZZM_UC_PRIVACY_GUARD",
                "server": "ctm-lin-srv",
                "agentMode": "hostgroups"
            }
        ]
    }
```

### Monitoring Function

📌 Get the agent and CCP status of your Control-M Servers, focused on Managed File Transfer.

👉 What it checks:

✅ List Control-M Servers

✅ Retrieve Agents & CCP

✅ Ping each Agent

✅ Test CCP with a live Agent

👉 Output is saved to:

- C:\ProgramData\engineer\data\ctm-monitoring.json
- /home/${USER}/.config/engineer/data/ctm-monitoring.json


``` markdown title="Linux"
engineer -m
```
``` markdown title="Linux"
engineer --monitoring
```

#### Result

📂 Example: [ctm-monitoring.json](example/ctm-monitoring.json)

### Help Function

📌 Get command help documentation

A log file is written to: 

- C:\ProgramData\engineer\logs\engineer.log
- /home/${USER}/.config/engineer/logs/engineer.log

``` markdown title="Linux"
engineer -h
```
``` markdown title="Linux"
engineer --help
```

### Output Function

📌 Combine the output function with:

- Inventory
- Monitoring
- Folders


📂 Logs: Log file are written to: 

- C:\ProgramData\engineer\logs\engineer.log
- /home/${USER}/.config/engineer/logs/engineer.log

``` markdown title="Linux"
engineer -o console
```
``` markdown title="Linux"
engineer --output console
```

#### Result

Print the data in json format to console.



### Expert Function

📌 The expert mode combines "monitoring" and "Folders".

👉 Output is saved to:

- C:\ProgramData\engineer\data\<filter-name>ctm-expert.json
- /home/${USER}/.config/engineer/data/<filter-name>ctm-expert.json

``` markdown title="Linux"
engineer -e -f <filter-name>
```
``` markdown title="Linux"
engineer -expert -f <filter-name>
```

#### Filter

The filter being applied is based on the engineer.json config file

📂 Example: [engineer.json](example/engineer.json)

``` markdown title="Filters"
"FILTERS": {
        "types": [
            {
                "type": "folders",
                "name": "ZZM",
                "folder": "ZZM_UC_MULTI*",
                "server": "ctm-lin-srv",
                "agentMode": "hostgroups"
            },
            {
                "type": "folders",
                "name": "PRIVACY_GUARD",
                "folder": "ZZM_UC_PRIVACY_GUARD",
                "server": "ctm-lin-srv",
                "agentMode": "hostgroups"
            }
        ]
    }
```

#### Result

📂 Example: [<filter-name>ctm-expert.json](example/privacy_guard-ctm-expert.json)

## Control-M AAPI

📌 Using the Config service, you can access, update, and add configuration data for the major components of the Control-M environment.

📌 The deploy service allows you to transfer job and configuration definitions to Control-M. Once a job is deployed, it will be scheduled by Control-M according to its scheduling criteria and dependencies. The deploy overwrites any existing definition of the same name. 

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


### Deployed Folders

The deploy folders::get command enables you to get details of folders that match a search criteria. 

``` markdown title="Get centralized deployed connection profile"
deploy folders::get -s <search query>
```

| Field	| Description |
| ------------- | ------------- |
| server | Name of Control-M/Server |
| agent | Name of Control-M/Agent |
| folder | Control-M Folder |
| job | Control-M Job |
| ctm | Control-M Enterprise Manager |

Filter applied: folder=<filter-name>

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


# Conclusion

CTM Engineer is a proactive solution designed to reduce workflow failures, minimize downtime, and enhance Control-M job execution reliability.

🚀 Get started today and streamline your Control-M workflow validation process! 🚀