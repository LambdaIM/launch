# storagenode service

## Description

view service status

## Usage
```
storagenode service [command]
```
## Available Commands

| Name| Description                                                                   |
| --------------- | --------------------- 
| list  | list all service status|
|  show | show service status|

## Examples
```
./storagenode service list
NAME                 LISTEN PORT                  STATUS
serverpub            172.11.159.11:15000         RUNNING
serverpriv           172.11.159.11:15001         RUNNING

./storagenode service show serverpub
NAME                 LISTEN PORT                  STATUS
serverpub            172.11.159.11:15000         RUNNING
```
