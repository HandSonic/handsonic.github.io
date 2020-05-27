---
layout: photo
title: 身份证识别系统搭建
date: 2020-05-25 18:25:17
tags: [AI]
---
# Day 2 - 身份证识别系统搭建

<a name="h2-url-1"></a>
## 身份证识别功能描述
RecognizeIdentityCard可以识别二代身份证关键字段内容，关键字段包括：姓名、性别、民族、身份证号、出生日期、地址信息、有效起始时间、签发机关，同时可输出身份证区域位置和人脸位置信息。<br />

<a name="h2-url-3"></a>
## 输入限制

- 图片格式：JPEG、JPG、PNG、BMP、GIF。
- 图像大小：图像大小不超过3M。
- 图像分辨率：不限制图片分辨率，但图片分辨率太高可能会导致API识别超时，超时时间为5秒。


<!-- more -->
<a name="h2-url-4"></a>
## 请求参数
| 名称 | 类型 | 是否必选 | 示例值 | 描述 |
| :--- | :--- | :--- | :--- | :--- |
| **Action** | String | 是 | RecognizeIdentityCard | 系统规定参数。取值：RecognizeIdentityCard。 |
| **ImageURL** | String | 是 | [https://viapi-demo.oss-cn-shanghai.aliyuncs.com/viapi-demo/images/DetectImageElements/detect-elements-src.png](https://viapi-demo.oss-cn-shanghai.aliyuncs.com/viapi-demo/images/DetectImageElements/detect-elements-src.png) | 图片URL地址。 |
| **Side** | String | 是 | face | 身份证正反面类型。<br />- face：正面。<br />- back：反面。<br /> |

<a name="dETIv"></a>
## 返回数据
| 名称 | 类型 | 示例值 | 描述 |
| :--- | :--- | :--- | :--- |
| Data | Struct |  | 返回的结果数据内容。 |
| BackResult | Struct |  | 反面照结果。 |
| EndDate | String | 19800101 | 有效期结束时间，格式：YYYYMMDD，例如19800101，即1980年01月01日。 |
| Issue | String | 杭州市公安局 | 签发机关。 |
| StartDate | String | 19700101 | 有效期起始时间，格式：YYYYMMDD，例如19800101，即1980年01月01日。 |
| FrontResult | Struct |  | 正面照结果。 |
| Address | String | 浙江省杭州市余杭区文一西路969号 | 地址信息。 |
| BirthDate | String | 20000101 | 出生日期，格式：YYYYMMDD，例如19800101，即1980年01月01日。 |
| CardAreas | Array |  | 身份证区域位置，四个顶点表示，顺序是逆时针（左上、左下、右下、右上）。 |
| X | Float | 165 | 身份证区域横坐标。 |
| Y | Float | 657 | 身份证区域纵坐标。 |
| FaceRectVertices | Array |  | 人脸位置，四个顶点表示。 |
| X | Float | 1024.6600341796875 | 人脸位置横坐标。 |
| Y | Float | 336.629638671875 | 人脸位置纵坐标。 |
| FaceRectangle | Struct |  | 人脸位置。 |
| Angle | Float | -90 | 表示矩形顺时针旋转的度数，范围-180~180。 |
| Center | Struct |  | 人脸矩形中心坐标。 |
| X | Float | 952 | 人脸矩形中心横坐标。 |
| Y | Float | 325.5 | 人脸矩形中心纵坐标。 |
| Size | Struct |  | 人脸矩形尺寸。 |
| Height | Float | 181.99 | 高度。 |
| Width | Float | 164.99 | 宽度。 |
| Gender | String | 男 | 性别。 |
| IDNumber | String | 1234567890 | 身份证号。 |
| Name | String | 张三 | 姓名。 |
| Nationality | String | 汉 | 民族。 |
| RequestId | String | D6C24839-91A7-41DA-B31F-98F08EF80CC0 | 请求ID。 |

<a name="s6XfA"></a>
## 返回数据示例

<br />请求示例<br />

```http
http(s)://ocr.cn-shanghai.aliyuncs.com/?Action=RecognizeIdentityCard
&ImageURL=https://viapi-demo.oss-cn-shanghai.aliyuncs.com/viapi-demo/images/DetectImageElements/detect-elements-src.png
&Side=face
&<公共请求参数>
```
正常返回示例<br />`XML` 格式<br />

```xml
<RequestId>D6C24839-91A7-41DA-B31F-98F08EF80CC0</RequestId>
<Data>
    <FrontResult>
        <Address>浙江省杭州市余杭区文一西路969号</Address>
        <Name>张三</Name>
        <Nationality>汉</Nationality>
        <IDNumber>1234567890</IDNumber>
        <Gender>男</Gender>
        <BirthDate>20000101</BirthDate>
        <FaceRectangle>
            <Angle>-90</Angle>
            <Center>
                <X>952</X>
                <Y>325.5</Y>
            </Center>
            <Size>
                <Height>181.99</Height>
                <Width>164.99</Width>
            </Size>
        </FaceRectangle>
        <CardAreas>
            <X>165</X>
            <Y>657</Y>
        </CardAreas>
        <CardAreas>
            <X>534</X>
            <Y>658</Y>
        </CardAreas>
        <CardAreas>
            <X>535</X>
            <Y>31</Y>
        </CardAreas>
        <CardAreas>
            <X>165</X>
            <Y>30</Y>
        </CardAreas>
        <FaceRectVertices>
            <X>1024.6600341796875</X>
            <Y>336.629638671875</Y>
        </FaceRectVertices>
        <FaceRectVertices>
            <X>906.6610717773438</X>
            <Y>336.14801025390625</Y>
        </FaceRectVertices>
        <FaceRectVertices>
            <x>907.1590576171875</x>
            <Y>214.1490478515625</Y>
        </FaceRectVertices>
        <FaceRectVertices>
            <x>1025.157958984375</x>
            <Y>214.63067626953125</Y>
        </FaceRectVertices>
    </FrontResult>
</Data>
```
`JSON` 格式<br />

```json
{
"RequestId": "D6C24839-91A7-41DA-B31F-98F08EF80CC0",
"Data": {
  "FrontResult": {
    "Address": "浙江省杭州市余杭区文一西路969号",
    "Name": "张三",
    "Nationality": "汉",
    "IDNumber": "1234567890",
    "Gender": "男",
    "BirthDate": "20000101",
    "FaceRectangle": {
      "Angle": -90,
      "Center": {
        "X": 952,
        "Y": 325.5
      },
      "Size": {
        "Height": 181.99,
        "Width": 164.99
      }
    },
    "CardAreas": [
      {
        "X": 165,
        "Y": 657
      },
      {
        "X": 534,
        "Y": 658
      },
      {
        "X": 535,
        "Y": 31
      },
      {
        "X": 165,
        "Y": 30
      }
    ],
    "FaceRectVertices": [
      {
        "X": 1024.6600341796875,
        "Y": 336.629638671875
      },
      {
        "X": 906.66107177734375,
        "Y": 336.14801025390625
      },
      {
        "x": 907.1590576171875,
        "Y": 214.1490478515625
      },
      {
        "x": 1025.157958984375,
        "Y": 214.63067626953125
      }
    ]
  }
}
}
```
<a name="title-52b-8of-slh"></a>
## JAVA SDK
引入POM包`<artifactId>ocr20191230</artifactId>`。
```xml
<dependency>
    <groupId>com.aliyun</groupId>
    <artifactId>ocr20191230</artifactId>
    <version>${aliyun.ocr.version}</version>
</dependency>
```

- **说明** 您可以通过`[https://mvnrepository.com/artifact/com.aliyun/](https://mvnrepository.com/artifact/com.aliyun/)**SDK包名称**`查看不同服务SDK的版本。例如`[https://mvnrepository.com/artifact/com.aliyun/aliyun-java-sdk-ocr](https://mvnrepository.com/artifact/com.aliyun/aliyun-java-sdk-ocr)`查看aliyun-java-sdk-ocr的版本。<br />
<a name="title-hoo-kpj-wv1"></a>
## 接入SDK
下面介绍新版本的参数构建和调用方法。

1. 引入资源。在pom.xml文件中添加Maven依赖安装java SDK。<br />
```xml
<dependency>
    <groupId>com.aliyun</groupId>
    <artifactId>aliyun-java-sdk-core</artifactId>
    <version>4.4.8</version>
</dependency>
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>fastjson</artifactId>
    <version>1.2.52</version>
</dependency>
<dependency>
    <groupId>com.aliyun</groupId>
    <artifactId>ocr20191230</artifactId>
    <version>${aliyun.ocr.version}</version>
</dependency>
<dependency>
    <groupId>com.aliyun</groupId>
    <artifactId>facebody20191230</artifactId>
    <version>${aliyun.facebody.version}</version>
</dependency>
<dependency>
    <groupId>com.aliyun</groupId>
    <artifactId>imagerecog20190930</artifactId>
    <version>${aliyun.imagerecog.version}</version>
</dependency>
<dependency>
    <groupId>com.aliyun</groupId>
    <artifactId>imageseg20191230</artifactId>
    <version>${aliyun.imageseg.version}</version>
</dependency>
<dependency>
    <groupId>com.aliyun</groupId>
    <artifactId>imageenhan20190930</artifactId>
    <version>${aliyun.imageenhan.version}</version>
</dependency>
<dependency>
    <groupId>com.aliyun</groupId>
    <artifactId>goodstech20191230</artifactId>
    <version>${aliyun.goodstech.version}</version>
</dependency>
<dependency>
    <groupId>com.aliyun</groupId>
    <artifactId>objectdet20191230</artifactId>
    <version>${aliyun.objectdet.version}</version>
</dependency>
<dependency>
    <groupId>com.aliyun</groupId>
    <artifactId>imgsearch20200320</artifactId>
    <version>${aliyun.imgsearch.version}</version>
</dependency>
<dependency>
    <groupId>com.aliyun</groupId>
    <artifactId>videorecog20200320</artifactId>
    <version>${aliyun.videorecog.version}</version>
</dependency>
<dependency>
    <groupId>com.aliyun</groupId>
    <artifactId>videoseg20200320</artifactId>
    <version>${aliyun.videoseg.version}</version>
</dependency>
<dependency>
    <groupId>com.aliyun</groupId>
    <artifactId>videoenhan20200320</artifactId>
    <version>${aliyun.videoenhan.version}</version>
</dependency>
```


1. 构建Client。示例如下：<br />
```java
// 你的accessKeyId
  config.accessKeyId="######"; 
  //你的accessKeySecret
  config.accessKeySecret="#######"; 
  config.type="access_key";
  config.regionId="cn-shanghai";
  config.endpointType="internal";
  Client client = new Client(config);
  config.endpoint="ocr.cn-shanghai.aliyuncs.com"; 
  //此处endpoint以文字识别为例。不同服务的Endpoint参见访问域名。
```

1. 调用服务。Client已经封装好需要调用的能力，且大多数API支持本地文件。
  - 使用URL
    - request：RecognizeIdentityCard
    - 方法：recognizeIdentityCard
    - 示例
```java
private static void RecognizeIdentityCard(Client client, RuntimeOptions runtimeOptions) throws Exception {
        try {
            RecognizeIdentityCardRequest req = new RecognizeIdentityCardRequest();
            req.imageURL="https://viapi-demo.oss-cn-shanghai.aliyuncs.com/viapi-demo/images/RecognizeIdentityCard/IdentityCard.jpg";
            RecognizeIdentityCardResponse rep = client.recognizeBankCard(req, runtimeOptions);
            System.out.println("身份证识别="+JSON.toJSONString(rep));
        }
        catch (TeaException e){
            System.out.println("身份证识别异常了");
            System.out.println(JSON.toJSONString(e.getData()));
        }
    }
```

  - 使用本地文件
    - request：RecognizIdentityCardAdvanceRequest
    - 方法：recognizeIdentityCardAdvance
    - 示例
```java
private static void RecognizeIdentityCardAdvance(Client client, RuntimeOptions runtimeOptions) throws Exception {
        try {
            RecognizeIdentityCardAdvanceRequest req = new RecognizeBankCardAdvanceRequest();
            InputStream inputStream = new FileInputStream(new File("/Users/robinqu/Library/IdentityCard.png"));
            req.imageURLObject=inputStream;
            RecognizeIdentityCardResponse rep = client.recognizeBankCardAdvance(req, runtimeOptions);
            System.out.println("银行卡识别="+JSON.toJSONString(rep));
        }
        catch (TeaException e){
            System.out.println("银行卡识别异常了");
            System.out.println(JSON.toJSONString(e.getData()));
        }
    }
```

1. 出现advance表示使用本地文件，没有则表示使用公网可以访问的URL。<br />
<a name="title-lgl-yad-gks"></a>
## 结果示例
对于同一个接口，如果SDK中包含类似xxxAdvanceRequest的结构，那么这个接口支持本地文件上传，否则不支持。<br />例如下图中ChangeImageSize是支持本地文件的，而RecolorImage则不支持本地文件，只支持OSS链接。
<a name="title-3a1-w9l-y5a"></a>
## 异常相关
如果调用发生异常，则异常信息会在`TeaException.getData()`中显示出来。<br />

```java
{
    "RequestId": "6B8A283F-DFFA-4F30-9DF1-A85D8609AD88",
    "HostId": "ocr.cn-shanghai.aliyuncs.com",
    "Code": "InvalidImage.Content",
    "Message": "Invalid Input - wrong category"
}
```
