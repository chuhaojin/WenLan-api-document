# 文澜API

## 用于获取图像的特征向量和文本的特征向量


### 1. [POST]获取图像的特征向量

* 方法描述：上传一张图片，获取图像的特征向量

* URL地址：http://120.92.50.21:6175/image_query

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
url = "http://120.92.50.21:6175/image_query"

r = requests.post(url, files=files)
print(r.text)
```

### 2. [GET]获取文本的特征向量

* 方法描述：上传一段文本，获取文本对应的特征向量

* URL地址：http://120.92.50.21:6175/text_query

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
url = "http://120.92.50.21:6175/text_query"
params = {"text":"中国人民大学位于北京中关村，是一所位于世界一流大学。"}

r = requests.get(url, params=params)
print(r.text)
```
