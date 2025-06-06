# nebulatimes-sdk-python

## Example

[DescribeOriginData](https://console.cloud.tencent.com/api/explorer?Product=cdn&Version=2018-06-06&Action=DescribeOriginData)

```go
# -*- coding: utf-8 -*-

import json
import types
from nebulatimesedge.common import credential
from nebulatimesedge.common.profile.client_profile import ClientProfile
from nebulatimesedge.common.profile.http_profile import HttpProfile
from nebulatimesedge.common.exception.nebulatimes_edge_sdk_exception import NebulatimesEdgeSDKException
from nebulatimesedge.cdn.v20250407 import cdn_client, models
try:
    # 实例化一个认证对象，入参需要传入腾讯云账户 SecretId 和 SecretKey，此处还需注意密钥对的保密
    # 代码泄露可能会导致 SecretId 和 SecretKey 泄露，并威胁账号下所有资源的安全性
    # 以下代码示例仅供参考，建议采用更安全的方式来使用密钥
    # 请参见：https://cloud.tencent.com/document/product/1278/85305
    # 密钥可前往官网控制台 https://console.cloud.tencent.com/cam/capi 进行获取
    cred = credential.Credential("ak", "sk")
    # 实例化一个http选项，可选的，没有特殊需求可以跳过
    httpProfile = HttpProfile()
    httpProfile.endpoint = "cdnapi.nebulatimes.com"

    # 实例化一个client选项，可选的，没有特殊需求可以跳过
    clientProfile = ClientProfile()
    clientProfile.httpProfile = httpProfile
    # 实例化要请求产品的client对象,clientProfile是可选的
    client = cdn_client.CdnClient(cred, "", clientProfile)

    # 实例化一个请求对象,每个接口都会对应一个request对象
    req = models.DescribeOriginDataRequest()
    params = {
        "Action":    "DescribeOriginData",
        "StartTime": "2025-04-01 00:00:00",
        "EndTime":   "2025-04-01 00:55:59",
        "Metric":    "flux",
    }
    req.from_json_string(json.dumps(params))

    # 返回的resp是一个DescribeOriginDataResponse的实例，与请求对象对应
    resp = client.DescribeOriginData(req)
    # 输出json格式的字符串回包
    print(resp.to_json_string())

except NebulatimesEdgeSDKException as err:
    print(err)
```
