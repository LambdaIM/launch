# 兼容 s3 的 gateway/网关

s3 网关(gateway) 利用minio提供了s3兼容的[api(部分)](https://docs.aws.amazon.com/AmazonS3/latest/API/Welcome.html) 来上传下载, 开发者可以针对s3api来开发应用。

也就是说，使用标准的s3的sdk或工具, 或者自己构造s3标准的请求可以跟s3网关交互 来操作lambda存储。



针对使用需求不同，提供了两种gateway：

* s3gw       针对单个订单进行操作，适用于一般用户
* lambgw  针对多个订单进行操作，支持multipart api，适用于开发者



##  s3gw 

一般用于用户转移数据，针对单个订单上传下载。



### 限制

目前阶段，lambda s3 网关支持的功能、接口也有限，基本的文件操作api之外的api大部分目前不支持。




s3网关使用minio来提供api，其中minio：

* 有若干api不支持，详细可以[参考](https://github.com/minio/minio/blob/master/docs/minio-limits.md#list-of-amazon-s3-apis-not-supported-on-minio)。
* s3 的文件version 不支持，可以[参考](https://github.com/minio/minio/pull/6494)



s3网关目前也不支持multipart api，所以在使用工具或sdk时候需要通过配置来避免来使用，下面的示例中将以64M为例。



### 配置与运行

针对s3网关的配置默认在 `~/.lambda_storagecli/config/user.toml` 的 `[gateway]` 部分，解释如下：
```ini
[gateway]
# 服务监听的地址
address = "127.0.0.1:9002"
# 用于访问服务的key
access_key = "accesskey"
secret_key = "secretkey"
```

若`user.toml`配置正常，可以在命令行调用 `./storagecli s3gw run  --account YOUR_ACCOUNT --broker.extra_order_id XXX` 来启动

启动的更多参数可以通过`./storagecli s3gw run -h`查看

### aws cli 使用示例

首先，先安装[awscli](https://docs.aws.amazon.com/cli/latest/userguide/installing.html).

之后，配置用于访问s3网关的key：
```
$ aws configure
AWS Access Key ID [None]: accesskey
AWS Secret Access Key [None]: secretkey
Default region name [None]:
Default output format [None]:
```

然后，配置multipart的阈值，`aws configure set default.s3.multipart_threshold 64MB`, 表示大于64M才使用multipart

之后就可以进行基本的文件操作了.
#### 创建bucket

`aws s3 --endpoint=http://localhost:9002/ mb s3://awstest`

#### 上传文件

`aws s3 --endpoint=http://localhost:9002/ cp /path/to/your/file s3://awstest`

#### 列出bucket内容

`aws s3 --endpoint=http://localhost:9002/ ls s3://awstest`

#### 下载文件

`aws s3 --endpoint=http://localhost:9002/ cp s3://awstest/your-file /tmp/new-file`


### aws python sdk 使用示例

首先，安装boto3 `pip install boto3`

然后，调整multipart的阈值

```python
#!/usr/bin/env python
# coding: utf-8

"""
refer https://docs.min.io/docs/how-to-use-aws-sdk-for-python-with-minio-server.html
"""

import boto3
from botocore.client import Config
from boto3.s3.transfer import TransferConfig

s3 = boto3.resource('s3',
                    endpoint_url='http://localhost:9002',
                    aws_access_key_id='accesskey',
                    aws_secret_access_key='secretkey',
                    config=Config(signature_version='s3v4'),
                    region_name='')


# create bucket
s3.Bucket('awstest').create()

# list bucket
print("buckets:", [bucket.name for bucket in s3.buckets.all()])

# upload file
# https://boto3.amazonaws.com/v1/documentation/api/latest/guide/s3.html#multipart-transfers
MB = 2 ** 20
cfg = TransferConfig(multipart_threshold=64*MB)
s3.Bucket('awstest').upload_file('/path/to/your/file','images/your-file', Config=cfg)

# list file
print("objects in bucket: awstest", [obj.key for obj in s3.Bucket('awstest2').objects.filter(Prefix='images/')])

# download file
s3.Bucket('awstest').download_file('images/your-file', '/tmp/newfile')
```



也可以使用minio提供的sdk，[minio文档](https://docs.min.io/docs/python-client-quickstart-guide)有详细的示例，这里不在赘述



## lambgw

针对开发者的gateway，支持 多订单、multipart api



### 配置与运行

针对s3网关的配置默认在 `~/.lambda_storagecli/config/user.toml` 的 `[gateway]` 部分，解释如下：

```ini
[gateway]
# 服务监听的地址
address = "127.0.0.1:9002"
# 用于访问服务的key
access_key = "accesskey"
secret_key = "secretkey"
```

若`user.toml`配置正常，可以在命令行调用 `./storagecli lambgw run  --account YOUR_ACCOUNT` 来启动

启动的更多参数可以通过`./storagecli lambgw run -h`查看



### 关于支持多订单

这里方式是将订单映射为bucket，实际的bucket则作为prefix参数的一部分，即：

* S3gw 上传的目标文件是 `bucket/prefix`，如 `test/a/b.txt`，其中`test`是bucket参数，`a/b.txt`是prefix参数

* lambgw 上传的目标文件是 `orderID/bucket+prefix`，如 `D9A585E80A92439D5DFFB384901F359A572F4E1F/test/a/b.txt`, 其中 `D9A585E80A92439D5DFFB384901F359A572F4E1F`是bucket参数，`test/a/b.txt`是prefix参数



使用awscli的上传示例：`aws s3 --endpoint http://127.0.0.1:9002 cp ~/Downloads/goland-2020.1.2.dmg s3://D9A585E80A92439D5DFFB384901F359A572F4E1F/test/`



⚠️ 订单的同步功能使用了 ListBucket api，即 购买新订单之后调用ListBucket，lambgw就能操作新订单了



### 关于支持multipart api

Multipart 是上传大文件就会自动触发的机制，通过将一个文件拆分成若干小文件分批、并发上传 可以提高上传速度。这个文件的大小是可以配置的，如awscli `aws configure set default.s3.multipart_threshold 64MB`  表示大于64M的文件才使用multipart



每个 multipart 都会在lambgw本地 组装成 一个临时的原始文件，然后上传到lambda存储网络。

⚠️需要注意，multipart的ID 在程序启动后会重新计算、临时文件会被清理，所以上传过程中 lambgw 停止会导致当前次的multipart失败，如果已经开始向lambda存储网络上传，则空间会被扣掉



#### list multipart

Ref https://docs.aws.amazon.com/cli/latest/reference/s3api/list-multipart-uploads.html



```
aws s3api --endpoint http://127.0.0.1:9002 list-multipart-uploads --bucket D9A585E80A92439D5DFFB384901F359A572F4E1F --prefix test/g

{
    "Uploads": [
        {
            "UploadId": "Upload1",
            "Key": "goland-2020.1.2.dmg",
            "Initiated": "0001-01-01T00:00:00+00:00",
            "StorageClass": "",
            "Owner": {
                "DisplayName": "",
                "ID": ""
            },
            "Initiator": {
                "ID": "",
                "DisplayName": ""
            }
        }
    ]
}
```



#### list parts

Ref https://docs.aws.amazon.com/AmazonS3/latest/API/API_ListParts.html

```
aws s3api --endpoint http://127.0.0.1:9002 list-parts --bucket D9A585E80A92439D5DFFB384901F359A572F4E1F --key test/goland-2020.1.2.dmg --upload-id Upload1

{
    "Parts": [
        {
            "PartNumber": 0,
            "LastModified": "2020-09-29T09:12:40.904000+00:00",
            "ETag": "\"22b473dc9bbf413468451df306446442\"",
            "Size": 8388608
        },
        {
            "PartNumber": 1,
            "LastModified": "2020-09-29T09:12:41.529000+00:00",
            "ETag": "\"de88583370841e2afc5e3fe9509f62b3\"",
            "Size": 8388608
        },
        {
            "PartNumber": 2,
            "LastModified": "2020-09-29T09:12:41.243000+00:00",
            "ETag": "\"4b5de2cb674fd13b7514438b6e309cb7\"",
            "Size": 8388608
        },
        {
            "PartNumber": 3,
            "LastModified": "2020-09-29T09:12:41.831000+00:00",
            "ETag": "\"e9652255edf52b2ce5470272d3f12261\"",
            "Size": 8388608
        },
        {
            "PartNumber": 4,
            "LastModified": "2020-09-29T09:12:40.974000+00:00",
            "ETag": "\"76387692018b541172d0e982997afc58\"",
            "Size": 8388608
        },
        {
            "PartNumber": 5,
            "LastModified": "2020-09-29T09:12:41.934000+00:00",
            "ETag": "\"fcb42b097acf568f0357605fd7ac1146\"",
            "Size": 8388608
        },
        {
            "PartNumber": 6,
            "LastModified": "2020-09-29T09:12:42.171000+00:00",
            "ETag": "\"28145c31976eca1e6c79d89043654241\"",
            "Size": 8388608
        },
        {
            "PartNumber": 7,
            "LastModified": "2020-09-29T09:12:41.058000+00:00",
            "ETag": "\"1dffe72d2f9db3731f117b1b90f7e7b8\"",
            "Size": 8388608
        },
        {
            "PartNumber": 8,
            "LastModified": "2020-09-29T09:12:42.307000+00:00",
            "ETag": "\"d38b3d60515be58829ca8e6e2f38aa5c\"",
            "Size": 8388608
        },
        {
            "PartNumber": 9,
            "LastModified": "2020-09-29T09:12:42.043000+00:00",
            "ETag": "\"18582234a64bc71894b23bc9c11ea042\"",
            "Size": 8388608
        },
        {
            "PartNumber": 10,
            "LastModified": "2020-09-29T09:12:42.478000+00:00",
            "ETag": "\"27009c0e9046b56a729e9b2a9a021cb5\"",
            "Size": 8388608
        }
    ],
    "Initiator": {
        "ID": "02d6176db174dc93cb1b899f7c6078f08654445fe8cf1b6ce98d8855f66bdbf4",
        "DisplayName": ""
    },
    "Owner": {
        "DisplayName": "",
        "ID": "02d6176db174dc93cb1b899f7c6078f08654445fe8cf1b6ce98d8855f66bdbf4"
    },
    "StorageClass": "STANDARD"
}

```

