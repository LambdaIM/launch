# minernode command
## Global flags of query commands

All query commands has these global flags. Their unique flags will be introduced later.


| Name, shorthand| type   | Required | Default Value         | Description                                                          |
| --------------- | ----   | -------- | --------------------- | -------------------------------------------------------------------- |
| --home     | string | false    | /root/.lambdacli                    | lambdacli home directory |
| --miner-home        | string    | false    | /root/.lambda_miner                    | config home directory |
| --help, -h      | string | false    |                       | help for minernode |


Examples
```
./minernode info  --miner-home /root/LambdaIM/storage/storage-feature_order_list_with_provider_status-984f41e-debug-03251653/.lambda_miner 
               version: 0.2.7_rc2-4-gd8a77f8
                dht id: 2u8PSj2PGt7TdR2ThuHMfH4k6KeEv5avgc4gbdKn3LTH
server.private_address: 172.11.159.11:14001
        server.address: 172.11.159.11:14000
  kad.external_address: 182.91.242.11:14000
    kad.bootstrap_addr: [182.91.242.11:13000]
         miner address: lambda12fldnycgpevw4gthq9w0zcfetpa9sn4d39wzlz (lambdamineroper12fldnycgpevw4gthq9w0zcfetpa9sn4d92z92l)
        mining address: lambda1kwk9qv7nncusukv7zx7j7j4mlt3eyrf6ecdwpu
      Ensure-level = 0: 1/6 of disk-space would be used for data-replicating
```



## Module command list
Each module provides a set of command line interfaces. Here we sort these commands by modules.

1. [info command](info.md)

2. [init command](init.md)

3. [run command](run.md)

4. [service command](service.md)

5. [show-address command](show-address.md)

6. [storage command](storage.md)

7. [upgrade command](upgrade.md)

8. [version command](version.md)

9. [order command](order.md)
