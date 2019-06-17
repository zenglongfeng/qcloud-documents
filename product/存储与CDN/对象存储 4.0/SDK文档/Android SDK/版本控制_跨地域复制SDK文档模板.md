## 简介

**版本控制**

| API | 操作名 | 操作描述 |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket versioning](https://cloud.tencent.com/document/product/436/19889) | 设置版本控制   | 设置存储桶的版本控制功能 |
| [GET Bucket versioning](https://cloud.tencent.com/document/product/436/19888) | 查询版本控制 | 查询存储桶的版本控制信息 |

**跨地域复制**

| API | 操作名 | 操作描述 |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket replication](https://cloud.tencent.com/document/product/436/19223) | 设置跨地域复制   | 设置存储桶的跨地域复制规则 |
| [GET Bucket replication](https://cloud.tencent.com/document/product/436/19222) | 查询跨地域复制 | 查询存储桶的跨地域复制规则 |
| [DELETE Bucket replication](https://cloud.tencent.com/document/product/436/19221) | 删除跨地域复制 | 删除存储桶的跨地域复制规则 |


## 版本控制
### 设置版本控制

#### 功能说明

设置指定存储桶的版本控制功能（PUT Bucket versioning）。

#### 方法原型
```
PutBucketVersioningResult putBucketVersioning(PutBucketVersioningRequest request)throws CosXmlClientException, CosXmlServiceException;
void putBucketVersionAsync(PutBucketVersioningRequest request, CosXmlResultListener cosXmlResultListener);
```

#### 请求示例

##### 开启版本控制
```
String bucket = "examplebucket-1250000000"; //格式：BucketName-APPID
PutBucketVersioningRequest putBucketVersioningRequest = new PutBucketVersioningRequest(bucket);
putBucketVersioningRequest.setEnableVersion(true); //true: 开启版本控制; false:暂停版本控制
// 使用同步方法
try {
    PutBucketVersioningResult putBucketVersioningResult = cosXmlService.putBucketVersioning(putBucketVersioningRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
// 使用异步回调请求
cosXmlService.putBucketVersionAsync(putBucketVersioningRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo PUT Bucket versioning success
        PutBucketVersioningResult putBucketVersioningResult = (PutBucketVersioningResult)result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo PUT Bucket versioning failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

#### 参数说明
| 参数名称| 描述  | 类型  |
| ----| ---- | ---- |
| bucket  | 存储桶名称，格式：BucketName-APPID,详情请参阅 [命名规范](https://cloud.tencent.com/document/product/436/13312#.E5.91.BD.E5.90.8D.E8.A7.84.E8.8C.83) | String                         |
| isEnable | 是否开启版本控制: true, 开启; false, 暂停 | boolean |
| headerKeys          |  签名是否校验 header                | `Set<String>` |
| cosXmlResultListener      | 结果回调        | CosXmlResultListener   |


#### 返回结果说明
通过 PutBucketVersioningResult 返回请求结果。

| 成员变量 | 类型 | 描述                                                     |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int  | HTTP Code， [200，300)之间表示操作成功，否则表示操作失败 |

> ?操作失败时，SDK 将抛出 [CosXmlClientException](https://cloud.tencent.com/document/product/436/34539#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8) 或 [CosXmlServiceException](https://cloud.tencent.com/document/product/436/34539#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8) 异常。


### 查询版本控制

#### 功能说明

查询指定存储桶的版本控制信息（GET Bucket versioning）。

#### 方法原型
```
GetBucketVersioningResult getBucketVersioning(GetBucketVersioningRequest request) throws CosXmlClientException, CosXmlServiceException;
void getBucketVersioningAsync(GetBucketVersioningRequest request, CosXmlResultListener cosXmlResultListener);
```

#### 请求示例
```
String bucket = "examplebucket-1250000000"; //格式：BucketName-APPID
GetBucketVersioningRequest getBucketVersioningRequest = new GetBucketVersioningRequest(bucket);
// 使用同步方法
try {
    GetBucketVersioningResult getBucketVersioningResult = cosXmlService.getBucketVersioning(getBucketVersioningRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
// 使用异步回调请求
cosXmlService.getBucketVersioningAsync(getBucketVersioningRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo GET Bucket versioning success
        GetBucketVersioningResult getBucketVersioningResult = (GetBucketVersioningResult)result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo GET Bucket versioning failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

#### 参数说明
| 参数名称| 描述  | 类型  |
| ----| ---- | ---- |
| bucket  | 存储桶名称，格式：BucketName-APPID,详情请参阅 [命名规范](https://cloud.tencent.com/document/product/436/13312#.E5.91.BD.E5.90.8D.E8.A7.84.E8.8C.83) | String                         |
| headerKeys          |  签名是否校验 header                | `Set<String>` |
| cosXmlResultListener      | 结果回调        | CosXmlResultListener   |


#### 返回结果说明
通过 GetBucketVersioningResult 返回请求结果。

| 成员变量 | 类型 | 描述                                                     |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int  | HTTP Code， [200，300)之间表示操作成功，否则表示操作失败 |
| versioningConfiguration | [VersioningConfiguration](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/normal/java/com/tencent/cos/xml/model/tag/VersioningConfiguration.java) | 返回指定账号下的存储桶版本控制的状态                         |

> ?操作失败时，SDK 将抛出 [CosXmlClientException](https://cloud.tencent.com/document/product/436/34539#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8) 或 [CosXmlServiceException](https://cloud.tencent.com/document/product/436/34539#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8) 异常。


## 跨地域复制
### 设置跨地域复制

#### 功能说明

设置指定存储桶的跨地域复制规则（PUT Bucket replication）。

#### 方法原型
```
PutBucketReplicationResult putBucketReplication(PutBucketReplicationRequest request)throws CosXmlClientException, CosXmlServiceException;
void putBucketReplicationAsync(PutBucketReplicationRequest request, CosXmlResultListener cosXmlResultListener);
```
#### 请求示例
```
String bucket = "examplebucket-1250000000"; //格式：BucketName-APPID
String ownerUin = "ownerUin"; //发起者身份标示:OwnerUin 
String subUin = "SubUin"; //发起者身份标示:SubUin 
PutBucketReplicationRequest putBucketReplicationRequest = new PutBucketReplicationRequest(bucket);
putBucketReplicationRequest.setReplicationConfigurationWithRole(ownerUin, subUin);
PutBucketReplicationRequest.RuleStruct ruleStruct = new PutBucketReplicationRequest.RuleStruct();
ruleStruct.id = "replication_01"; //用来标注具体 Rule 的名称
ruleStruct.isEnable = true; //标识 Rule 是否生效 :true, 生效； false, 不生效
ruleStruct.appid = "1250000000"; //appid
ruleStruct.region = Region.AP_Beijing.getRegion(); //目标存储桶地域信息
ruleStruct.bucket = "destExamplebucket-1250000000";  // 目标存储桶
ruleStruct.prefix = "34"; //前缀匹配策略，
putBucketReplicationRequest.setReplicationConfigurationWithRule(ruleStruct);

// 使用同步方法
try {
    PutBucketReplicationResult putBucketReplicationResult = cosXmlService.putBucketReplication(putBucketReplicationRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}   
// 使用异步回调请求
cosXmlService.putBucketReplicationAsync(putBucketReplicationRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo PUT Bucket replication success
        PutBucketReplicationResult putBucketReplicationResult = (PutBucketReplicationResult)result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo PUT Bucket replication failed because of CosXmlClientException or CosXmlServiceException...
    }
});

```

#### 参数说明
| 参数名称| 描述  | 类型  |
| ----| ---- | ---- |
| bucket  | 存储桶名称，格式：BucketName-APPID,详情请参阅 [命名规范](https://cloud.tencent.com/document/product/436/13312#.E5.91.BD.E5.90.8D.E8.A7.84.E8.8C.83) | String                         |
| ownerUin  |发起者身份标示:OwnerUin  | String |
| subUin  |发起者身份标示:SubUin    | String |
| ruleStruct  |签名是否校验请求 url 中查询参数    | RuleStruct |
| queryParameterKeys  |签名是否校验请求 url 中查询参数    | `Set<String>` |
| headerKeys          |  签名是否校验 header                | `Set<String>` |
| cosXmlResultListener      | 结果回调        | CosXmlResultListener   |


#### 返回结果说明
通过 PutBucketReplicationResult 返回请求结果。

| 成员变量 | 类型 | 描述                                                     |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int  | HTTP Code， [200，300)之间表示操作成功，否则表示操作失败 |

> ?操作失败时，SDK 将抛出 [CosXmlClientException](https://cloud.tencent.com/document/product/436/34539#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8) 或 [CosXmlServiceException](https://cloud.tencent.com/document/product/436/34539#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8) 异常。


### 查询跨地域复制

#### 功能说明

查询指定存储桶的跨地域复制规则（GET Bucket replication）。

#### 方法原型
```
GetBucketReplicationResult getBucketReplication(GetBucketReplicationRequest request)throws CosXmlClientException, CosXmlServiceException;
void getBucketReplicationAsync(GetBucketReplicationRequest request, CosXmlResultListener cosXmlResultListener);
```

#### 请求示例
```
String bucket = "examplebucket-1250000000"; //格式：BucketName-APPID
GetBucketReplicationRequest getBucketReplicationRequest = new GetBucketReplicationRequest(bucket);
// 使用同步方法
try {
    GetBucketReplicationResult getBucketReplicationResult = cosXmlService.getBucketReplication(getBucketReplicationRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
// 使用异步回调请求
cosXmlService.getBucketReplicationAsync(getBucketReplicationRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo GET Bucket replication success
        GetBucketReplicationResult getBucketReplicationResult = (GetBucketReplicationResult)result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo GET Bucket replication failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

#### 参数说明
| 参数名称| 描述  | 类型  |
| ----| ---- | ---- |
| bucket  | 存储桶名称，格式：BucketName-APPID,详情请参阅 [命名规范](https://cloud.tencent.com/document/product/436/13312#.E5.91.BD.E5.90.8D.E8.A7.84.E8.8C.83) | String                         |
| headerKeys          |  签名是否校验 header                | `Set<String>` |
| cosXmlResultListener      | 结果回调        | CosXmlResultListener   |

#### 返回结果说明
通过 GetBucketReplicationResult 返回请求结果。

| 成员变量 | 类型 | 描述                                                     |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int  | HTTP Code， [200，300)之间表示操作成功，否则表示操作失败 |
| replicationConfiguration | [ReplicationConfiguration](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/normal/java/com/tencent/cos/xml/model/tag/ReplicationConfiguration.java) | 返回指定账号下的存储桶的跨区域配置信息                         |

> ?操作失败时，SDK 将抛出 [CosXmlClientException](https://cloud.tencent.com/document/product/436/34539#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8) 或 [CosXmlServiceException](https://cloud.tencent.com/document/product/436/34539#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8) 异常。


### 删除跨地域复制

#### 功能说明

删除指定存储桶的跨地域复制规则（DELETE Bucket replication）。

#### 方法原型
```
DeleteBucketReplicationResult deleteBucketReplication(DeleteBucketReplicationRequest request)throws CosXmlClientException, CosXmlServiceException;
void deleteBucketReplicationAsync(DeleteBucketReplicationRequest request, CosXmlResultListener cosXmlResultListener);
```

#### 请求示例
```
String bucket = "examplebucket-1250000000"; //格式：BucketName-APPID
DeleteBucketReplicationRequest deleteBucketReplicationRequest = new DeleteBucketReplicationRequest(bucket);
// 使用同步方法
try {
    DeleteBucketReplicationResult deleteBucketReplicationResult = cosXmlService.deleteBucketReplication(deleteBucketReplicationRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
// 使用异步回调请求
cosXmlService.deleteBucketReplicationAsync(deleteBucketReplicationRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo DELETE Bucket replication success
        DeleteBucketReplicationResult deleteBucketReplicationResult = (DeleteBucketReplicationResult)result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo DELETE Bucket replication failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

#### 参数说明
| 参数名称| 描述  | 类型  |
| ----| ---- | ---- |
| bucket  | 存储桶名称，格式：BucketName-APPID,详情请参阅 [命名规范](https://cloud.tencent.com/document/product/436/13312#.E5.91.BD.E5.90.8D.E8.A7.84.E8.8C.83) | String                         |
| headerKeys          |  签名是否校验 header                | `Set<String>` |
| cosXmlResultListener      | 结果回调        | CosXmlResultListener   |


#### 返回结果说明
通过 DeleteBucketReplicationResult 返回请求结果。

| 成员变量 | 类型 | 描述                                                     |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int  | HTTP Code， [200，300)之间表示操作成功，否则表示操作失败 |

> ?操作失败时，SDK 将抛出 [CosXmlClientException](https://cloud.tencent.com/document/product/436/34539#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.BC.82.E5.B8.B8) 或 [CosXmlServiceException](https://cloud.tencent.com/document/product/436/34539#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.BC.82.E5.B8.B8) 异常。

