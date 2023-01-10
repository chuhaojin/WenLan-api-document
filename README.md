# 文澜1.0 API已经在2023年1月9日停用，感谢大家关注！
### 你可以在本地部署文澜模型抽特征，推荐使用repo：(https://github.com/chuhaojin/BriVL-BUA-applications)[https://github.com/chuhaojin/BriVL-BUA-applications].

# 文澜1.0 API文档

## 悟道·文澜简介
为了更进一步地推动相关领域的研究，北京智源人工智能研究院、中国人民大学和中科院计算所的研究团队在中国人民大学高瓴人工智能学院执行院长文继荣教授的带领下合作开展了大规模中文多模态预训练模型的研究，并发布了第一代悟道·文澜，旨在发掘预训练模型在中文通用多模态数据上的理解能力。


文澜团队推出的第一代图文互检模型在论文中叫做BriVL (Bridging Vision and Language)，经过一系列的实验和探索，文澜团队采用了双塔结构作为BriVL 的基本架构。现阶段的文澜已初具规模，具备强大的视觉-语言检索能力和一定的常识理解能力。初始版本的BriVL 在AIC-ICC和RUC-CAS-WenLan上的评测结果已经超过了UNITER和CLIP。


论文地址：https://arxiv.org/abs/2103.06561


BriVL首先使用了独立的语言和视觉编码器提取语言和视觉信息的特征向量，并对其分别执行序列池化和多层感知机操作，从而将视觉特征和语言特征映射为同一空间下的高维特征向量。采用这样的双塔结构，既可以抽取单模态特征，也可以灵活地将多模态语义特征在同一特征空间下进行度量。

## 获取图像的特征向量和文本的特征向量


### 1. [POST]获取图像的特征向量

* 方法描述：上传一张图片，获取图像的特征向量

~~* URL地址：http://120.92.50.21:6175/image_query~~

~~* URL地址：http://180.76.186.10:6175/image_query (2022年2月7日迁移至新IP)~~

* URL地址：http://buling.wudaoai.cn/image_query (2022年6月8日迁移至新地址)

* 请求类型：POST

* 请求参数


| 字段 | 说明 | 类型 | 备注 | 是否必填 |
|:-----:|:-----:|:-----:|:-----:|:-----:|
| image|要抽取特征向量的图片|file|支持png, jpg, jpeg格式的文件|是|


* 返回字段说明
   
| 字段 | 说明 | 类型 | 备注 |
|:-----:|:-----:|:-----:|:-----:|
| emb_dim | 特征向量的维度 | int | 一般为2048维 |
| emb_type | 特征向量的类别 | string | 有image和text两种类型，在此处为image |
| embedding | 特征向量 | list | 由浮点数组成的一个list |

* 返回结果示例

```python
{
  	emb_dim:2048,
  	emb_type:'image',
  	embedding:[0.1,0.2,0.3,...,204.8]
}
```



* 调用示例

```python
import requests
files = {"image": open("test.jpg", "rb")}
url = "http://buling.wudaoai.cn/image_query"

r = requests.post(url, files=files)
print(r.json())
```

### 2. [GET]获取文本的特征向量

* 方法描述：上传一段文本，获取文本对应的特征向量

~~* URL地址：http://180.76.186.10:6175/text_query~~

* URL地址：http://buling.wudaoai.cn/text_query (2022年6月8日迁移至新地址)
* 请求类型：GET

* 请求参数


| 字段 | 说明 | 类型 | 备注 | 是否必填 |
|:-----:|:-----:|:-----:|:-----:|:-----:|
| text |要获取特征向量的文本| string|  |是|


* 返回字段说明
   
| 字段 | 说明 | 类型 | 备注 |
|:-----:|:-----:|:-----:|:-----:|
| emb_dim | 特征向量的维度 | int | 一般为2048维 |
| emb_type | 特征向量的类别 | string | 有image和text两种类型，在此处为text |
| embedding | 特征向量 | list | 由浮点数组成的一个list |


* 返回结果示例

```python
{
  	emb_dim:2048,
  	emb_type:'text',
  	embedding:[0.1,0.2,0.3,...,204.8]
}
```


* 调用示例

```python
import requests
url = "http://buling.wudaoai.cn/text_query"
params = {"text":"中国人民大学位于北京中关村，是一所世界一流大学。"}

r = requests.get(url, params=params)
print(r.json())
```

* MORE

除了本repo里公布的这个非正式文澜1.0 API外，也可以从智源社区获取同样的服务：https://wudaoai.cn/home

需要注意的是，智源提供的API所使用的模型已经在2021年6月底更新为了2.0版本，已经和本repo提供的API不一致。

