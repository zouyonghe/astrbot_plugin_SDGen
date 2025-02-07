# astrbot_plugin_SDGen

## 介绍
用于图片生成的AstrBot插件，使用Stable Diffusion WebUI的API进行图片生成

## 安装
- 插件商店直接安装
- 复制 `https://github.com/zouyonghe/astrbot_plugin_SDGen` 导入

## 工作流
**使用LLM生成提示词 -> 使用WebUI生成图像 -> 图像增强（可选） -> 输出图像**

## 配置参数说明

### WebUI API地址
- **类型**: `string`
- **描述**: WebUI API 地址
- **默认值**: `http://127.0.0.1:7860`
- **提示**: 需要包含 `http://` 或 `https://` 前缀

### 全局负面提示词
- **类型**: `string`
- **描述**: 负面提示词，会自动附加到所有生成请求
- **默认值**: `(worst quality, low quality:1.4), deformed, bad anatomy`
- **提示**: 可自行定义，以优化生成效果

### 详细回复开关
- **类型**: `bool`
- **描述**: 控制回复的详略程度
- **默认值**: `true`
- **提示**: `true` 时，将输出生成步骤，否则只输出图片

### 启用高分辨率处理
- **类型**: `bool`
- **描述**: 是否启用高分辨率处理
- **默认值**: `false`
- **提示**: `true` 时启用高分辨率处理

### 图像尺寸
- **宽度 (`width`)**:
  - **类型**: `int`
  - **默认值**: `512`
  - **可选值**: `[512, 768, 1024]`
- **高度 (`height`)**:
  - **类型**: `int`
  - **默认值**: `512`
  - **可选值**: `[512, 768, 1024]`

### 采样步数 (`steps`)
- **类型**: `int`
- **默认值**: `20`
- **范围**: `10 - 50`

### 采样方法 (`sampler`)
- **类型**: `string`
- **默认值**: `DPM++ 2M`
- **可选值**: `Euler a`, `Euler`, `Heun`, `DPM2`, `DPM2 a`, `DPM++ 2M`, `DPM++ 2M SDE`, `DPM++ 2M SDE Heun`, `DPM++ 2S a`, `DPM++ 3M SDE`, `DDIM`, `LMS`, `PLMS`, `UniPC`

### 提示词权重 (`cfg_scale`)
- **类型**: `int`
- **默认值**: `7`
- **范围**: `1 - 20`
- **提示**:
  - `1-3`: 图像更随机，可能会偏离提示词描述，但创造性更高。
  - `10-15`: 图像更严格遵循提示词，但可能导致细节过度锐化或不自然。
  - **推荐范围**: `7-12`

### 上采样算法 (`upscaler`)
- **类型**: `string`
- **默认值**: `ESRGAN_4x`
- **可选值**: `Latent`, `Latent(antialiased)`, `Latent(bicubic)`, `Latent(bicubic antialiased)`, `Latent(nearest)`, `Latent(nearest-exact)`, `None`, `Lanczos`, `Nearest`, `DAT x2`, `DAT x3`, `DAT x4`, `ESRGAN_4x`, `LDSR`, `R-ESRGAN 4x+`, `R-ESRGAN 4x+ Anime6B`, `ScuNET`, `SCUNET PSNR`, `SwinlR_4x`
- **提示**: 选择用于图像放大的算法，如 ESRGAN、R-ESRGAN 等

### 图像放大倍数 (`upscale_factor`)
- **类型**: `int`
- **默认值**: `2`
- **范围**: `1 - 8`
- **提示**: 常见值为 `2`, `4` 等

### 图像生成模型
- **类型**: `string`
- **描述**: 选择用于生成的图像模型
- **默认值**: `""`
- **提示**: 默认为空，使用 `/sd model list` 获取

### LMM附加限制
- **类型**: `string`
- **描述**: LMM 生成提示词时的附加限制
- **默认值**: `""`
- **提示**: 例如 `任何被判断为色情的提示词都应该被替换，避免出现色情内容`

### 关于Stable Diffusion WebUI的部署建议
1. 克隆仓库
```bash
git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui
cd stable-diffusion-webui
```

2. 检查python版本
<span style="color:red">（不要直接运行webui.sh)</span>

```bash
python -V
```
如果python版本高于3.10，例如3.11、3.12、3.13，请使用conda（anaconda或miniconda）或者mamba创建环境（可能也可以用pyenv设置，暂未验证）
```bash
conda create -n webui python=3.10
conda activate webui
# 取消激活时使用 conda deactivate
conda install pip
```
3. 安装依赖
```bash
pip install -r requirements.txt
```
4. 首次运行，会安装大量模型、依赖等，需要一段时间
```bash
./webui.sh
```
5. 安装插件（可选）
- 汉化插件 https://github.com/hanamizuki-ai/stable-diffusion-webui-localization-zh_Hans.git 或 https://github.com/VinsonLaro/stable-diffusion-webui-chinese
- 超分辨率插件 https://github.com/Coyote-A/ultimate-upscale-for-automatic1111
- 提示词插件 https://github.com/Physton/sd-webui-prompt-all-in-one/tree/main

6. 以API方式启动webui
```bash
./webui.sh --listen --port 7860 --api      # 带webui的方式启动
#./webui.sh --listen --port 7860 --nowebui # 不带webui，仅API方式启动
```
# 支持
QQ： 1259085392
- 请尽可能自己debug，实在无法解决的问题再寻求帮助
- 任何代码方面问题，请随时发issues

[帮助文档](https://astrbot.soulter.top/center/docs/%E5%BC%80%E5%8F%91/%E6%8F%92%E4%BB%B6%E5%BC%80%E5%8F%91/
)
