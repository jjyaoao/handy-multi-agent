# 附录：支持的模型

## 1. 文本模型

### 1.1 OpenAI模型
- **GPT-4**
  - 功能：文本生成、对话、代码生成等
  - 特点：强大的推理能力和知识储备
  - 适用场景：复杂任务处理、创意写作、代码开发

- **GPT-3.5-turbo**
  - 功能：文本生成、对话、简单任务处理
  - 特点：响应速度快、成本较低
  - 适用场景：日常对话、简单问答、基础任务

### 1.2 开源模型
- **Llama 2**
  - 功能：文本生成、对话
  - 特点：开源可本地部署
  - 适用场景：通用对话、文本生成

- **Qwen**
  - 功能：中文文本处理、对话
  - 特点：中文能力强、部署灵活
  - 适用场景：中文应用场景

## 2. 多模态模型

### 2.1 视觉-语言模型
- **GPT-4V**
  - 功能：图像理解、多模态对话
  - 特点：强大的视觉理解能力
  - 适用场景：图像描述、视觉问答

- **Qwen-VL**
  - 功能：中文图文理解
  - 特点：中文场景适配好
  - 适用场景：中文图文应用

### 2.2 语音模型
- **Whisper**
  - 功能：语音识别、转录
  - 特点：多语言支持
  - 适用场景：语音转文字、字幕生成

## 3. 模型使用示例

### 3.1 文本模型调用
```python
from camel.models import ModelFactory

# 创建GPT-4模型实例
gpt4_model = ModelFactory.create(
    model_name="gpt-4",
    api_key="your_api_key"
)

# 创建对话
response = gpt4_model.generate(
    prompt="请介绍CAMEL框架的主要特点。",
    max_tokens=500
)
```

### 3.2 多模态模型调用
```python
from camel.models import MultiModalModel
from PIL import Image

# 创建GPT-4V模型实例
gpt4v_model = MultiModalModel(
    model_name="gpt-4v",
    api_key="your_api_key"
)

# 加载图像
image = Image.open("example.jpg")

# 生成图像描述
description = gpt4v_model.analyze_image(
    image=image,
    prompt="请描述这张图片的主要内容。"
)
```

## 4. 模型选择建议

### 4.1 场景匹配
- **简单对话**：GPT-3.5-turbo
- **复杂任务**：GPT-4
- **本地部署**：Llama 2、Qwen
- **多模态任务**：GPT-4V、Qwen-VL

### 4.2 成本考虑
- **开发测试**：GPT-3.5-turbo
- **生产环境**：根据具体需求选择
- **离线场景**：开源模型

### 4.3 性能要求
- **响应速度**：GPT-3.5-turbo
- **准确性**：GPT-4
- **并发处理**：本地部署模型

## 5. 最佳实践

### 5.1 模型配置
```python
# 模型配置示例
model_config = {
    'temperature': 0.7,
    'max_tokens': 1000,
    'top_p': 0.9,
    'frequency_penalty': 0.0,
    'presence_penalty': 0.0
}

# 创建模型实例
model = ModelFactory.create(
    model_name="gpt-4",
    api_key="your_api_key",
    **model_config
)
```

### 5.2 错误处理
```python
try:
    response = model.generate(prompt)
except ModelError as e:
    # 处理模型错误
    print(f"模型错误: {e}")
except APIError as e:
    # 处理API错误
    print(f"API错误: {e}")
except Exception as e:
    # 处理其他错误
    print(f"其他错误: {e}")
```

### 5.3 性能优化
```python
# 批量处理示例
async def batch_process(prompts):
    tasks = []
    async with ModelPool() as pool:
        for prompt in prompts:
            task = pool.generate(prompt)
            tasks.append(task)
        results = await asyncio.gather(*tasks)
    return results
```

## 6. 注意事项

1. **API密钥管理**
   - 使用环境变量
   - 实施访问控制
   - 定期更新密钥

2. **错误处理**
   - 实现重试机制
   - 设置超时控制
   - 做好日志记录

3. **资源管理**
   - 控制并发请求
   - 管理token使用
   - 监控API限额

4. **成本控制**
   - 选择适当模型
   - 优化prompt设计
   - 实施缓存机制

通过合理选择和配置模型，我们可以在不同场景下实现最优的应用效果。在实际使用中，建议根据具体需求和约束条件，选择最适合的模型和配置方案。 