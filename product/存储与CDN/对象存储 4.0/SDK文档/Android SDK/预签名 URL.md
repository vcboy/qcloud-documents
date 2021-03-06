## 简介
本文档提供关于获取对象请求预签名 URL 的示例代码。

## SDK API 参考

SDK 所有接口的具体参数与方法说明，请参考 [SDK API 参考](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/)。

## 获取预签名 URL

#### 示例代码一：获取预签名上传 URL

[//]: # (.cssg-snippet-get-presign-upload-url)
```java
try {
    String bucket = "examplebucket-1250000000"; //存储桶名称
    String cosPath = "exampleobject"; //即对象在存储桶中的位置标识符。
    String method = "PUT"; //请求 HTTP 方法
    PresignedUrlRequest presignedUrlRequest = new PresignedUrlRequest(bucket
            , cosPath) {
        @Override
        public RequestBodySerializer getRequestBody()
                throws CosXmlClientException {
            //用于计算 put 等需要带上 body 的请求的签名 URL
            return RequestBodySerializer.string("text/plain",
                    "this is test");
        }
    };
    presignedUrlRequest.setRequestMethod(method);

    String urlWithSign = cosXmlService.getPresignedURL(presignedUrlRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
}
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/qcloud-sdk-android/tree/master/Demo/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/ObjectPresignUrl.java) 查看。

#### 示例代码二：获取预签名下载 URL

[//]: # (.cssg-snippet-get-presign-download-url)
```java
try {
    String bucket = "examplebucket-1250000000"; //存储桶名称
    String cosPath = "exampleobject"; //即对象在存储桶中的位置标识符。
    String method = "GET"; //请求 HTTP 方法.
    PresignedUrlRequest presignedUrlRequest = new PresignedUrlRequest(bucket
            , cosPath);
    presignedUrlRequest.setRequestMethod(method);

    String urlWithSign = cosXmlService.getPresignedURL(presignedUrlRequest);

} catch (CosXmlClientException e) {
    e.printStackTrace();
}
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/qcloud-sdk-android/tree/master/Demo/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/ObjectPresignUrl.java) 查看。
