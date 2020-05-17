# AWS S3 usage with Python & Boto3 library
Published at: 10/2/2020
---

Cloud based object storage has become an important part of any software application stack in recent times. [AWS S3](https://aws.amazon.com/s3/) has become the de-facto choice for this use case.


## Use with python
- The official sdk for python is [Boto3](https://boto3.amazonaws.com/v1/documentation/api/latest/index.html) which provide API for using AWS S3.

### Create boto3 configuration using AWS credentials
- Below is an example of basic boto3 configuration. More details, options & best practices can be found in [https://boto3.amazonaws.com/v1/documentation/api/latest/guide/configuration.html](https://boto3.amazonaws.com/v1/documentation/api/latest/guide/configuration.html)
 
```
import boto3

s3_resource = boto3.resource(
    "s3",
    aws_access_key_id="**********",
    aws_secret_access_key="**********",
)
```
## S3 File download

### Get file objects of a Bucket
- Set `bucket` variable as name of the S3 bucket
- Set `prefix` variable as name of S3 folder structure prefix. For eg. for file name like `s3://bucketname/[clientid]/file1.csv`, clientid can be used as prefix to get only files starting with a particular clientid.
- Using the above, we can use the `list_objects_v2` method to get a list of matching file objects
```
obj = s3_resource.meta.client.list_objects_v2(Bucket=bucket, Prefix=prefix)
all_keys_obj = obj['Contents']
```    
- The output of the above step is a list of s3 objects, like below
```
[
    {'Key': '*****', 'LastModified': datetime.datetime(2020, 3, 3, 12, 16, 16, tzinfo=tzutc()), 'ETag': '"*****"', 'Size': 869061, 'StorageClass': 'STANDARD', 'Owner': {'ID': '*****'}},
    ....
    {'Key': '*****', 'LastModified': datetime.datetime(2020, 3, 3, 12, 18, 10, tzinfo=tzutc()), 'ETag': '"*****"', 'Size': 23333915, 'StorageClass': 'STANDARD', 'Owner': {'ID': '*****'}}
]
```