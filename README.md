# Gemini API Key 怎么用？Gemini API 接口调用与 OpenAI 兼容接入教程

很多开发者搜索“**Gemini API Key 怎么用**”“**Gemini API 接口怎么调用**”“**Gemini 国内怎么接入**”，本质上都是想把 Gemini 接入到自己的程序中。

例如：

- 在网站中加入 AI 问答
- 开发 Gemini 聊天机器人
- 使用 Gemini 分析图片
- 让 Gemini 总结长文本
- 接入企业知识库
- 使用 Gemini 编写和分析代码
- 通过统一接口切换 GPT、Claude、Gemini 等模型

先简单说明：

- **Gemini API Key** 用于验证 API 请求身份
- Gemini API 可以用于文本生成、对话、代码、图片理解和文档分析等任务
- 如果直接调用原生接口，需要按照对应官方格式构造请求
- 如果使用支持 OpenAI 兼容格式的 Gemini 中转 API，可以复用现有的 OpenAI SDK 和项目代码
- 国内开发者在选择接入方式时，还需要考虑网络环境、模型支持、计费、限流和服务稳定性

**国内推荐 API 中转站平台：**

> AI API 中转站平台地址：<https://quanzil.com>

> AI API 中转站平台地址：<https://quanzil.net>

本文将介绍 Gemini API Key 的配置方法、Gemini API 接口调用流程，以及如何通过 OpenAI 兼容格式接入 Gemini。

---

## Gemini API Key 是什么

Gemini API Key 是调用 Gemini API 时使用的访问凭证。

当你的程序向 Gemini API 发送请求时，平台需要通过 API Key 判断：

- 当前请求来自哪个账户
- 当前账户是否有调用权限
- 请求是否使用了正确的模型
- 当前账户是否有余额或配额
- 请求是否超过频率限制

API Key 本身不是模型名称，也不是 API 地址。

一次完整的 API 调用通常需要三个核心信息：

```text
API Key + API 请求地址 + 模型名称
```

例如：

```text
API Key：YOUR_API_KEY
Base URL：https://your-api-domain.com/v1
模型名称：gemini-2.0-flash
```

具体的模型名称和接口地址，需要以你使用的平台实际支持情况为准。

---

## Gemini API 可以做什么

Gemini API 适用于多种 AI 应用场景。

### 文本生成

可以用于：

- 文章写作
- 营销文案
- 产品介绍
- 邮件生成
- 标题生成
- 内容改写
- 语法纠错

---

### 多轮对话

可以开发：

- AI 助手
- 智能客服
- 在线问答
- 企业内部助手
- 教育辅导工具
- 售前咨询机器人

---

### 代码处理

Gemini API 可以用于：

- 生成代码
- 解释代码
- 修复错误
- 编写测试
- 代码重构
- SQL 生成
- 接口文档生成

---

### 文档和长文本分析

常见用途包括：

- 合同摘要
- 报告总结
- 会议纪要整理
- 产品需求分析
- PDF 内容提取
- 文档问答
- 多份资料对比

---

### 图片理解

支持多模态能力的 Gemini 模型可以用于：

- 图片问答
- 截图分析
- 商品图片识别
- 表格截图理解
- UI 页面分析
- 图片文字提取
- 图文内容总结

是否支持图片输入，以及具体参数格式，要以接口文档为准。

---

## Gemini API 国内接入方式

目前开发者常见的 Gemini 接入方式主要有两类。

### 直接调用原生 Gemini API

这种方式一般需要：

- 使用官方 SDK 或接口格式
- 配置 API Key
- 按照原生请求结构发送参数
- 自行处理访问、限流和错误
- 根据官方返回结构解析结果

这种方式适合熟悉 Gemini 原生接口、只使用 Gemini 模型，并且具备稳定访问环境的团队。

---

### 使用 Gemini API 中转站

另一种方式是使用支持 Gemini 的 API 中转服务。

常见特点包括：

- 提供统一 API 地址
- 支持 OpenAI 兼容格式
- 可以使用统一的 Bearer Key
- 方便切换多个模型
- 减少不同 SDK 之间的适配工作
- 便于在 GPT、Claude、Gemini 等模型之间进行测试

如果你的项目已经基于 OpenAI API 开发，使用兼容接口通常会更容易迁移。

---

## Gemini API Key 应该放在哪里

API Key 建议放在服务端环境变量中。

Linux 或 macOS 环境可以这样设置：

```bash
export GEMINI_API_KEY="YOUR_API_KEY"
```

Python 中读取：

```python
import os

api_key = os.getenv("GEMINI_API_KEY")
print(api_key)
```

Node.js 中读取：

```javascript
const apiKey = process.env.GEMINI_API_KEY;
```

不建议采用以下方式：

```javascript
const apiKey = "YOUR_API_KEY";
```

尤其不要把真实 API Key 直接写进：

- 前端 JavaScript
- Android APK
- iOS 客户端
- GitHub 仓库
- 公共博客
- 截图和教程
- 浏览器可见的请求代码

因为前端代码会暴露给用户，任何人都可能复制你的 Key 进行调用。

---

## Gemini API Key 请求头怎么写

如果使用 OpenAI 兼容格式，通常使用以下请求头：

```bash
Authorization: Bearer YOUR_API_KEY
```

完整示例：

```bash
curl https://your-api-domain.com/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -d '{
    "model": "gemini-2.0-flash",
    "messages": [
      {
        "role": "user",
        "content": "请介绍 Gemini API。"
      }
    ]
  }'
```

不同平台的鉴权方式可能存在差异。

有些原生 Gemini 接口可能使用其他参数方式，例如查询参数或特定请求头。因此，调用前一定要确认当前平台的接口文档。

---

## Gemini API 最小调用示例

### cURL 调用示例

下面是 OpenAI 兼容格式的 Gemini API 调用方式：

```bash
curl https://your-api-domain.com/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -d '{
    "model": "gemini-2.0-flash",
    "messages": [
      {
        "role": "user",
        "content": "请用三句话介绍 Gemini API 的用途。"
      }
    ],
    "temperature": 0.7,
    "max_tokens": 500
  }'
```

请求中的几个字段分别表示：

- `model`：要调用的模型
- `messages`：对话消息
- `temperature`：输出随机性
- `max_tokens`：最大输出长度

---

### Python requests 示例

```python
import os
import requests

url = "https://your-api-domain.com/v1/chat/completions"
api_key = os.getenv("GEMINI_API_KEY")

payload = {
    "model": "gemini-2.0-flash",
    "messages": [
        {
            "role": "user",
            "content": "请解释 Gemini API 和普通网页聊天有什么区别。"
        }
    ],
    "temperature": 0.7,
    "max_tokens": 500
}

headers = {
    "Content-Type": "application/json",
    "Authorization": f"Bearer {api_key}"
}

response = requests.post(
    url,
    headers=headers,
    json=payload,
    timeout=60
)

print(response.status_code)
print(response.json())
```

建议在正式项目中增加异常处理：

```python
import os
import requests

url = "https://your-api-domain.com/v1/chat/completions"
api_key = os.getenv("GEMINI_API_KEY")

payload = {
    "model": "gemini-2.0-flash",
    "messages": [
        {
            "role": "user",
            "content": "请总结 Gemini API 的主要特点。"
        }
    ],
    "max_tokens": 500
}

headers = {
    "Content-Type": "application/json",
    "Authorization": f"Bearer {api_key}"
}

try:
    response = requests.post(
        url,
        headers=headers,
        json=payload,
        timeout=60
    )

    response.raise_for_status()
    data = response.json()

    print(data)

except requests.exceptions.Timeout:
    print("请求超时，请稍后重试")

except requests.exceptions.HTTPError as error:
    print("HTTP 请求失败：", error)

except requests.exceptions.RequestException as error:
    print("请求异常：", error)
```

---

## 使用 OpenAI SDK 调用 Gemini

如果 Gemini API 中转站支持 OpenAI 兼容格式，可以直接使用 OpenAI SDK。

安装依赖：

```bash
pip install openai
```

调用代码：

```python
import os
from openai import OpenAI

client = OpenAI(
    api_key=os.getenv("GEMINI_API_KEY"),
    base_url="https://your-api-domain.com/v1"
)

response = client.chat.completions.create(
    model="gemini-2.0-flash",
    messages=[
        {
            "role": "system",
            "content": "你是一名专业的技术顾问。"
        },
        {
            "role": "user",
            "content": "请说明 Gemini API 适合哪些业务场景。"
        }
    ],
    temperature=0.7,
    max_tokens=600
)

print(response.choices[0].message.content)
```

如果你原来调用的是 GPT，很多情况下只需要调整：

```python
client = OpenAI(
    api_key="YOUR_API_KEY",
    base_url="https://your-api-domain.com/v1"
)
```

以及：

```python
model="gemini-2.0-flash"
```

这样可以减少项目重构成本。

---

## Gemini API 流式输出怎么调用

如果你的应用是聊天机器人，通常希望模型逐字返回内容，而不是等待完整结果生成后一次性显示。

如果平台支持流式调用，可以使用：

```python
import os
from openai import OpenAI

client = OpenAI(
    api_key=os.getenv("GEMINI_API_KEY"),
    base_url="https://your-api-domain.com/v1"
)

stream = client.chat.completions.create(
    model="gemini-2.0-flash",
    messages=[
        {
            "role": "user",
            "content": "请介绍如何设计一个 Gemini API 应用。"
        }
    ],
    stream=True
)

for chunk in stream:
    content = chunk.choices[0].delta.content

    if content:
        print(content, end="", flush=True)
```

流式输出适合：

- AI 聊天页面
- 在线写作工具
- 实时客服
- 代码生成界面
- 长回答场景

使用流式接口时，要注意处理：

- 连接中断
- 空数据块
- 客户端取消请求
- 前端拼接内容
- 请求超时
- 最终响应状态

---

## Gemini API 如何传递系统提示词

系统提示词可以用于设置模型角色、回答风格和输出规则。

示例：

```python
messages = [
    {
        "role": "system",
        "content": "你是一名专业的中文技术编辑，回答要准确、简洁、结构清晰。"
    },
    {
        "role": "user",
        "content": "请解释什么是 Gemini API。"
    }
]
```

常见的系统提示词要求包括：

- 使用中文回答
- 只输出 JSON
- 不要编造不存在的信息
- 回答控制在指定字数内
- 扮演客服、程序员或产品经理
- 使用 Markdown 格式
- 给出分步骤解决方案

系统提示词不是越长越好。

建议只保留真正影响模型行为的规则，避免增加无关内容和调用成本。

---

## Gemini API 如何返回 JSON

如果你需要将模型结果交给程序继续处理，可以要求返回 JSON。

提示词示例：

```text
请分析下面的商品描述，并只返回合法 JSON。

返回字段：
name：商品名称
category：商品分类
summary：商品摘要
keywords：关键词数组

不要输出 Markdown，不要添加额外解释。
```

Python 示例：

```python
import json
from openai import OpenAI

client = OpenAI(
    api_key="YOUR_API_KEY",
    base_url="https://your-api-domain.com/v1"
)

response = client.chat.completions.create(
    model="gemini-2.0-flash",
    messages=[
        {
            "role": "system",
            "content": "你只返回合法 JSON，不要输出其他内容。"
        },
        {
            "role": "user",
            "content": "请提取这段文本中的标题、分类和关键词。"
        }
    ]
)

content = response.choices[0].message.content

try:
    data = json.loads(content)
    print(data)
except json.JSONDecodeError:
    print("模型返回的内容不是合法 JSON：")
    print(content)
```

正式项目中仍然建议做 JSON 校验，因为模型可能偶尔添加解释文字或 Markdown 代码块。

---

## Gemini API 图片理解怎么调用

如果你要让 Gemini 分析图片，需要确认当前模型和平台是否支持多模态输入。

常见应用包括：

- 分析网页截图
- 识别商品图片
- 读取表格截图
- 解释流程图
- 分析 UI 设计
- 提取图片中的文字
- 判断图片内容

不同 API 平台对图片输入的格式可能不同，常见方式包括：

- 图片 URL
- Base64
- 多模态 `content` 数组
- 单独的图片字段

OpenAI 兼容格式示例可能类似：

```python
from openai import OpenAI

client = OpenAI(
    api_key="YOUR_API_KEY",
    base_url="https://your-api-domain.com/v1"
)

response = client.chat.completions.create(
    model="gemini-2.0-flash",
    messages=[
        {
            "role": "user",
            "content": [
                {
                    "type": "text",
                    "text": "请描述这张图片中的主要内容。"
                },
                {
                    "type": "image_url",
                    "image_url": {
                        "url": "https://example.com/image.jpg"
                    }
                }
            ]
        }
    ]
)

print(response.choices[0].message.content)
```

注意：不同中转平台对多模态参数的支持可能不同，实际使用前需要查看平台文档。

---

## Gemini 模型怎么选择

### Gemini Flash 类模型

适合：

- 普通聊天
- 简单问答
- 内容改写
- 文本摘要
- 分类任务
- 高并发客服
- 成本敏感型场景
- 基础图片理解

如果你刚开始开发 Gemini 应用，可以先使用 Flash 类模型测试。

---

### Gemini Pro 类模型

适合：

- 复杂分析
- 高质量内容生成
- 代码开发
- 长文档理解
- 企业知识库问答
- 多步骤任务
- 对回答质量要求较高的业务

Pro 类模型的成本和响应速度可能与轻量模型不同，建议根据实际任务测试。

---

### Gemini 多模态模型

如果项目需要处理图片、视频、表格或文档，需要选择支持对应输入类型的模型。

使用前要确认：

- 是否支持图片输入
- 是否支持文件输入
- 支持哪些图片格式
- 单个文件大小限制
- 是否支持视频或 PDF
- 多模态输入如何计费

---

## Gemini API 成本怎么控制

### 不要发送过长的历史消息

多轮对话如果持续发送完整历史记录，输入 token 会不断增加。

可以采用以下方式：

- 只保留最近几轮对话
- 定期将历史内容压缩成摘要
- 删除无关消息
- 对长文档使用检索
- 只发送当前问题相关内容

---

### 限制输出长度

可以通过参数限制输出：

```json
{
  "max_tokens": 500
}
```

同时在提示词中说明：

```text
请在 300 字以内完成回答。
```

---

### 按任务选择模型

建议使用模型分层策略：

- 简单任务使用 Flash
- 复杂任务使用 Pro
- 图片和文档任务选择多模态模型
- 高价值业务使用更高能力模型
- 批量任务优先使用轻量模型

---

### 对重复请求进行缓存

对于相同或相似的问题，可以加入缓存机制。

适合缓存的内容包括：

- FAQ
- 产品介绍
- 固定术语解释
- 常见客服问题
- 标准化摘要
- 重复的分类任务

缓存不仅可以降低成本，也能提高响应速度。

---

## Gemini API 常见报错

### 401 错误

`401 Unauthorized` 一般表示 API Key 或鉴权信息不正确。

检查：

```bash
Authorization: Bearer YOUR_API_KEY
```

同时确认：

- API Key 没有多余空格
- Key 没有失效
- 请求头名称正确
- Base URL 配置正确
- 当前接口使用的是正确的 Key

---

### 403 错误

`403 Forbidden` 通常表示没有权限。

可能原因：

- 账户没有对应模型权限
- 当前 Key 权限不足
- 账户状态异常
- 平台限制了当前请求
- 调用了不支持的接口

建议检查账户权限、模型列表和平台说明。

---

### 404 错误

`404 Not Found` 通常表示地址或路径错误。

常见问题：

- Base URL 写错
- 缺少 `/v1`
- endpoint 路径错误
- 把完整请求地址重复拼接
- 当前平台不支持该调用格式

常见 OpenAI 兼容路径：

```text
https://your-api-domain.com/v1/chat/completions
```

---

### 429 错误

`429 Too Many Requests` 通常表示频率过高或余额、配额不足。

处理建议：

- 降低请求频率
- 限制并发数量
- 增加指数退避重试
- 设置请求队列
- 检查账户余额
- 切换轻量模型
- 对相同请求进行缓存

---

### 500、502、503、504 错误

这些错误通常与服务端、上游接口或网络超时有关。

建议：

- 设置合理的超时时间
- 对临时错误进行重试
- 记录错误日志
- 减少单次请求长度
- 降低并发
- 准备备用模型或降级方案

不要对所有错误无限重试，否则可能导致请求堆积或重复计费。

---

## Gemini API 中转站怎么选

选择 Gemini API 中转站时，可以重点关注以下方面。

### 是否支持 OpenAI 兼容格式

如果支持 OpenAI 兼容接口，你可以更方便地复用现有 SDK 和代码。

---

### 是否支持常用 Gemini 模型

查看平台是否提供你需要的模型，例如：

- Flash 类模型
- Pro 类模型
- 多模态模型
- 长上下文模型

模型名称以平台实际列表为准。

---

### 是否有详细的开发文档

至少应该能够查到：

- Base URL
- API Key 配置方式
- 请求示例
- 模型列表
- 参数说明
- 错误代码
- 流式调用方式
- 多模态调用方式

---

### 是否支持调用记录和余额管理

开发过程中建议关注：

- 请求次数
- Token 消耗
- 调用模型
- 响应耗时
- 错误比例
- 账户余额

这些数据可以帮助你控制成本和定位问题。

---

## Gemini API 和其他大模型如何切换

如果项目使用 OpenAI 兼容格式，可以将模型调用封装成一个函数。

```python
from openai import OpenAI

def call_model(
    api_key,
    base_url,
    model,
    prompt
):
    client = OpenAI(
        api_key=api_key,
        base_url=base_url
    )

    response = client.chat.completions.create(
        model=model,
        messages=[
            {
                "role": "user",
                "content": prompt
            }
        ],
        max_tokens=800
    )

    return response.choices[0].message.content
```

调用 Gemini：

```python
result = call_model(
    api_key="YOUR_API_KEY",
    base_url="https://your-api-domain.com/v1",
    model="gemini-2.0-flash",
    prompt="请介绍 Gemini API。"
)

print(result)
```

切换到其他模型时，只需要改变：

```python
model="another-model"
```

这样可以降低业务代码对单个模型的依赖。

---

## 常见问题

### Gemini API Key 怎么配置？

建议将 API Key 设置为环境变量：

```bash
export GEMINI_API_KEY="YOUR_API_KEY"
```

然后在程序中读取：

```python
import os

api_key = os.getenv("GEMINI_API_KEY")
```

不要直接将真实 Key 写入前端或公开代码仓库。

---

### Gemini API 可以使用 OpenAI SDK 吗？

如果使用的中转站支持 OpenAI 兼容格式，一般可以通过配置 `base_url` 的方式使用 OpenAI SDK。

但具体支持哪些参数，需要查看平台文档。

---

### Gemini API 国内调用需要注意什么？

主要需要关注：

- 网络访问稳定性
- API Key 安全
- 模型是否可用
- 接口地址是否正确
- 请求频率限制
- 账户余额和配额
- 多模态参数是否支持

如果希望简化接入，可以选择提供 Gemini 模型调用能力的 API 中转站。

---

### Gemini Flash 和 Pro 哪个更好？

没有绝对答案。

- Flash 更适合速度快、成本低和高并发场景
- Pro 更适合复杂任务、高质量生成和深度分析

建议使用真实业务数据进行测试，再决定默认模型。

---

### Gemini API 可以做图片识别吗？

支持多模态能力的 Gemini 模型可以处理图片理解任务。

但需要确认：

- 当前模型是否支持图片输入
- 平台是否支持图片 URL 或 Base64
- 请求格式是否符合平台要求
- 图片大小和格式是否有限制

---

### Gemini API 能不能做企业知识库？

可以。

常见方案是：

1. 用户提出问题
2. 检索知识库
3. 获取相关文档片段
4. 将文档片段放进提示词
5. 调用 Gemini API
6. 返回回答和参考依据

对于大规模知识库，建议使用 RAG，而不是把全部文档直接发送给模型。

---

## 总结

**Gemini API Key 怎么用？Gemini API 接口怎么调用？**

基本流程可以概括为：

1. 准备 Gemini API Key
2. 配置正确的 Base URL
3. 选择可用的 Gemini 模型
4. 按接口格式发送请求
5. 解析返回内容
6. 增加超时、重试和日志
7. 根据业务控制模型和成本

如果你只是测试 Gemini，可以先使用 cURL 或 Python 发起一个最小请求。

如果你的项目已经使用 OpenAI SDK，或者后续还需要接入 GPT、Claude、DeepSeek 等模型，可以优先选择支持 OpenAI 兼容格式的 Gemini API 中转站。
