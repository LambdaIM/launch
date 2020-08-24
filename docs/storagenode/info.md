# storagenode info

## Description

about storage information

## Usage

```
storagenode info [command]
```

## Available Commands

| Name| Description                                                                   |
| --------------- | --------------------- 
| disk  | show storage disk info|
|  index | storage index info|
|  network | show storage network info|

## Show storage disk info

## Usage

```
storagenode info disk [flags]
```
## Flags

| Name, shorthand| Default   | Description | Required                                                                  |
| --------------- | ----   | -------- | --------------------- 
|--local-mode   |  | local mode, no contract extra remote service |
|--prune   |  | prune order data |

## Examples

```
./storagenode info  disk  --local-mode   
               version:  0.2.7_rc2-13-gdbcabcf-debug
  storage.storage_name:  t4s5
      storage.data_dir:  [/data2/storage/store /data3/storage/store /data/storage/store /data4/store]

Disk                 |Total   |Used   |Free    |Order                                    |Occupied |SafeCleanup?
/data2/storage/store |18 GiB  |14 GiB |4.6 GiB |0A0250B4143BD1F69DFBEBD98ADDDFEF99397511 |240 MiB  |false
                     |        |       |        |82EB03450C809F3F8867C8D30BDD42D6C8802E92 |2.7 GiB  |false
/data/storage/store  |187 GiB |23 GiB |164 GiB |82EB03450C809F3F8867C8D30BDD42D6C8802E92 |3.3 GiB  |false
                     |        |       |        |BB549FB804062AB89A6AE3C3C8B6E1188EA9F36C |128 MiB  |false
                     |        |       |        |F083BC34E5CC1E2E6DBD20F0A274A70252DCCBC3 |1.3 GiB  |false


./storagenode info  disk  --prune 
             blockTime:  2020-04-11 14:01:27 UTC
               version:  0.2.7_rc2-13-gdbcabcf-debug
  storage.storage_name:  t4s5
      storage.data_dir:  [/data2/storage/store /data3/storage/store /data/storage/store /data4/storage/store]

Disk                 | Total   |Used   |Free    |Order                                    |Occupied |SafeCleanup?
/data2/storage/store |18 GiB  |14 GiB |4.6 GiB |0A0250B4143BD1F69DFBEBD98ADDDFEF99397511 |240 MiB  |false
                     |        |       |        |82EB03450C809F3F8867C8D30BDD42D6C8802E92 |2.7 GiB  |false
/data3/storage/store |18 GiB  |18 GiB |0 B     |A60DF26061D0A98D4F9338AAC8A0683BD0927429 |18 GiB   |true
/data/storage/store  |187 GiB |50 GiB |136 GiB |51866A6BBB6E2EE819D921D85094E76D1D54410A |116 MiB  |true
                      |        |       |        |82EB03450C809F3F8867C8D30BDD42D6C8802E92 |3.3 GiB  |false
                      |        |       |        |A60DF26061D0A98D4F9338AAC8A0683BD0927429 |11 GiB   |true
                      |        |       |        |A62C0765A24CB031686B06A6C1EB0F508E625F1E |9.4 GiB  |true
                      |        |       |        |BB549FB804062AB89A6AE3C3C8B6E1188EA9F36C |128 MiB  |false
                      |        |       |        |D7A999F935192C313913FEF25EC9F3B2EC199819 |8.3 GiB  |true
                      |        |       |        |F083BC34E5CC1E2E6DBD20F0A274A70252DCCBC3 |1.3 GiB  |false
/data4/storage/store  |37 GiB  |34 GiB |2.7 GiB |A60DF26061D0A98D4F9338AAC8A0683BD0927429 |7.0 GiB  |true



```

# storage index info
## Usage

```
 storagenode info index [flags]
```

## Flags

| Name, shorthand| Default   | Description | Required                                                                  |
| --------------- | ----   | -------- | --------------------- 
|--rebuild    |  | rebuild local storage index |

## Examples

```
./storagenode info  index --rebuild
This could take long time depends on your file trees...

indexing  /lambda/data/store
 /EAB528223F77D8AB7894298F01A2280D42085BF8/test > 762 records

/root/.lambda_storage/storagedb   updated.
762 records in total
time elasped: 9.59795602s

```
# show storage network info
## Usage

```
show storage network info
```

## Flags

| Name, shorthand| Default   | Description | Required                                                                  |
| --------------- | ----   | -------- | --------------------- 
| --dht-id    |  | show dht id |
| --test    |  | test if the configuration is correct |

## Examples

```
./storagenode info network --dht-id
ETj21L2dWgxPfCr5ocRDYeRXb9rREjWM5B2gox6UatYP

./storagenode info network --test
               version: 0.2.7_rc2-debug
                dht id: ETj21L2dWgxPfCr5ocRDYeRXb9rREjWM5B2gox6UatYP
  storage.storage_name: t4
 storage.miner_address: 172.11.159.11:14001 	 successful
server.private_address: 172.11.159.11:15001 	 successful
        server.address: 172.11.159.11:15000 	 successful
  kad.external_address: 182.91.242.11:15000 	 successful
    kad.bootstrap_addr: [182.91.242.11:13000] 	  successful
```
