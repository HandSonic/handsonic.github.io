---
title: 电子相册搭建
date: 2020-05-27 08:25:17
tags: [AI]
---

# 电子相册搭建（人脸、表情识别）

<a name="bYdf1"></a>
# 
<a name="pIH1V"></a>
## 表情识别功能描述
RecognizeExpression可以检测和识别图片中人脸的表情。表情种类为：neutral（中性）、happiness（高兴）、surprise（惊讶）、sadness（伤心）、anger（生气）、disgust（厌恶）、fear（害怕）。
<a name="Gc5dO"></a>
### 输入限制

- 图片分辨率：分辨率要求大于5×5像素。<br />
- 图片大小：图片大小不超过3M。<br />
- 人脸尺寸：建议大于64×64像素。<br />
<a name="N2jIo"></a>
<!-- more -->
### 请求参数
| 名称 | 类型 | 是否必选 | 示例值 | 描述 |
| :--- | :--- | :--- | :--- | :--- |
| **Action** | String | 是 | RecognizeExpression | 系统规定参数。取值：RecognizeExpression。 |
| **ImageURL** | String | 是 | [https://viapi-test.oss-cn-shanghai.aliyuncs.com/test/facebody/RecognizeBrow/brow.jpg](https://viapi-test.oss-cn-shanghai.aliyuncs.com/test/facebody/RecognizeBrow/brow.jpg) | 图片URL地址。 |

<a name="0pq1t"></a>
### 返回数据
| 名称 | 类型 | 示例值 | 描述 |
| :--- | :--- | :--- | :--- |
| Data | Struct |  | 返回的结果数据内容。 |
| Elements | Array |  | 各个子元素的识别结果。 |
| Expression | String | surprise | 表情类别。枚举类型：neutral、happiness、surprise、sadness、anger、disgust、fear。 |
| FaceProbability | Float | 0.99651491641998291 | 检测结果的概率，取值范围为0~1。 |
| FaceRectangle | Struct |  | 人脸区域信息。 |
| Height | Integer | 174 | 人脸区域的高度。 |
| Left | Integer | 196 | 人脸区域的左上角x坐标。 |
| Top | Integer | 41 | 人脸区域的左上角y坐标。 |
| Width | Integer | 121 | 人脸区域的宽度。 |
| RequestId | String | E1C4C576-1799-4079-A934-15BC406A54EF | 请求ID。 |

<a name="IzluL"></a>
### 示例
请求示例<br />http(s)://facebody.cn-shanghai.aliyuncs.com/?Action=RecognizeExpression<br />&ImageURL=https://viapi-test.oss-cn-shanghai.aliyuncs.com/test/facebody/RecognizeBrow/brow.jpg<br />&<公共请求参数><br />返回示例（JSON）<br />{<br />  "RequestId": "E1C4C576-1799-4079-A934-15BC406A54EF",<br />  "Data": {<br />    "Elements": [<br />      {<br />        "Expression": "surprise",<br />        "FaceRectangle": {<br />          "Left": 196,<br />          "Top": 41,<br />          "Height": 174,<br />          "Width": 121<br />        },<br />        "FaceProbability": "0.99651491641998291"<br />      }<br />    ]<br />  }<br />}
<a name="ArwUu"></a>
## 场景识别功能描述
RecognizeScene可以识别图像中的场景环境，支持数十种常见场景，包括：人物、会议室、公路、其他、办公室、动物、卧室、商场、地铁、夜景、天空、婚礼、室内、室外、小河、山峰、广场、建筑、户外、手机、旅行、日出、日落、显示器、树林、植物、水果、汽车、沙滩、沙漠、海滨、游乐场、湖、演出、火车、烧烤、物品、 狗、猫、美食、聚餐、自行车、船、花、草地、蔬菜、街景、街道、运动、运动场、露营、飞机、餐厅、鱼、鸟。
<a name="cNn71"></a>
### 输入限制

- 请求格式：JPEG、JPG、PNG、BMP。<br />
- 图像大小：图像大小不超过3M。<br />
- 图像分辨率：图片要求5×5像素以上。<br />
<a name="Q6hz5"></a>
### 请求参数
| 名称 | 类型 | 是否必选 | 示例值 | 描述 |
| :--- | :--- | :--- | :--- | :--- |
| **Action** | String | 是 | RecognizeScene | 系统规定参数。取值：RecognizeScene。 |
| **ImageURL** | String | 是 | [https://viapi-demo.oss-cn-shanghai.aliyuncs.com/viapi-demo/images/DetectImageElements/detect-elements-src.png](https://viapi-demo.oss-cn-shanghai.aliyuncs.com/viapi-demo/images/DetectImageElements/detect-elements-src.png) | 图片URL地址。当前仅支持上海地域的OSS链接，如何生成图片URL请参见[生成URL](https://help.aliyun.com/document_detail/155645.html)。 |

<a name="7XxLO"></a>
### 返回数据
| 名称 | 类型 | 示例值 | 描述 |
| :--- | :--- | :--- | :--- |
| Data | Struct |  | 返回的结果数据内容。 |

| Tags | Array |  | tags输出，对应正常、性感、色情三个标签的输出分数，每个标签会输出`confidence`和`value`两个参数，`value`是标签名称，`confidence`是对应分数，范围0~100。
输出标签数量最少1个，最多5个，如果某个类别标签未输出，则对应的`confidence`为零。 |
| Confidence | Float | 97 | 分数，范围0~100。 |
| Value | String | 人物 | 标签名称。 |
| RequestId | String | 3602D349-D892-43EA-ADF5-13DC714F3547 | 请求ID。 |
<a name="WB9e6"></a>
### 示例
请求示例<br />http(s)://imagerecog.cn-shanghai.aliyuncs.com/?Action=RecognizeScene<br />&ImageURL=https://viapi-demo.oss-cn-shanghai.aliyuncs.com/viapi-demo/images/DetectImageElements/detect-elements-src.png<br />&<公共请求参数><br />返回示例（JSON）<br />{<br />    "RequestId": "3602D349-D892-43EA-ADF5-13DC714F3547",<br />    "Data": {<br />        "Tags": [<br />            {<br />                "Confidence": 97,<br />                "Value": "人物"<br />            },<br />            {<br />                "Confidence": 11,<br />                "Value": "其他"<br />            },<br />            {<br />                "Confidence": 11,<br />                "Value": "运动"<br />            },<br />            {<br />                "Confidence": 11,<br />                "Value": "物品"<br />            },<br />            {<br />                "Confidence": 11,<br />                "Value": "演出"<br />            }<br />        ]<br />    }<br />}
