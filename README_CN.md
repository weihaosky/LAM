# LAM: 官方Pytorch实现

[![Website](https://raw.githubusercontent.com/prs-eth/Marigold/main/doc/badges/badge-website.svg)](https://aigc3d.github.io/projects/LAM/) 
[![arXiv Paper](https://img.shields.io/badge/📜-arXiv:2503-10625)](https://arxiv.org/pdf/2502.17796)
[![HuggingFace](https://img.shields.io/badge/🤗-HuggingFace_Space-blue)](https://huggingface.co/spaces/3DAIGC/LAM)
[![ModelScope](https://img.shields.io/badge/%20ModelScope%20-Space-blue)](https://www.modelscope.cn/studios/Damo_XR_Lab/LAM_Large_Avatar_Model)
[![Apache License](https://img.shields.io/badge/📃-Apache--2.0-929292)](https://www.apache.org/licenses/LICENSE-2.0)

<p align="center">
  <img src="./assets/images/logo.jpeg" width="20%">
</p>

### <p align="center"> LAM: Large Avatar Model for One-shot Animatable Gaussian Head </p>

#####  <p align="center"> Yisheng He*, Xiaodong Gu*, Xiaodan Ye, Chao Xu, Zhengyi Zhao, Yuan Dong†, Weihao Yuan†, Zilong Dong, Liefeng Bo </p>

#####  <p align="center"> 阿里巴巴通义实验室</p>

####  <p align="center"> **"单图秒级打造超写实3D数字人"** </p>

<p align="center">
  <img src="./assets/images/teaser.jpg" width="100%">
</p>

## 核心亮点 🔥🔥🔥
- **单图秒级生成超写实3D数字人化身！**
- **WebGL跨平台超实时驱动渲染！手机跑满120FPS！**
- **低延迟实时交互对话数字人SDK！**

## 📢 最新动态

**[2025年4月21日]** 我们开源了 WebGL交互数字人SDK：[OpenAvatarChat](https://github.com/HumanAIGC-Engineering/OpenAvatarChat) (including LLM, ASR, TTS, Avatar), 使用这个SDK可以自由地与我们的LAM-3D数字人进行实时对话 ! 🔥 <br>

**[2025年4月19日]** 我们开源了 [Audio2Expression](https://github.com/aigc3d/LAM_Audio2Expression) 模型, 用这个模型可以语音驱动我们的LAM数字人 ! 🔥 <br>

**[2025年4月10日]** 我们发布了 [ModelScope](https://www.modelscope.cn/studios/Damo_XR_Lab/LAM_Large_Avatar_Model) 演示程序 ! <br>

### 待办清单
- [x] 开源在VFHQ和Nersemble数据集上训练的LAM-small模型.
- [x] 部署Huggingface演示程序.
- [x] 部署Modelscope演示程序.
- [ ] 开源在自有大数据集上训练的LAM-large模型.
- [ ] 开源跨平台WebGL驱动渲染引擎.
- [x] 开源语音驱动模型: Audio2Expression.
- [x] 开源交互对话数字人SDK，包括LLM, ASR, TTS, Avatar.



## 🚀 快速开始
### 环境设置
```bash
git clone git@github.com:aigc3d/LAM.git
cd LAM
# Install with Cuda 12.1
sh  ./scripts/install/install_cu121.sh
# Or Install with Cuda 11.8
sh ./scripts/install/install_cu118.sh
```

### 模型权重

| 模型   | 训练数据集                  | HuggingFace | OSS | 重建时间 | A100 (A & R) |   XiaoMi 14 Phone (A & R)          |
|---------|--------------------------------|----------|----------|---------------------|-----------------------------|-----------|
| LAM-20K | VFHQ                          | TBD       | TBD      | 1.4 s               | 562.9FPS                    | 110+FPS   |
| LAM-20K | VFHQ + NeRSemble                | [Link](https://huggingface.co/3DAIGC/LAM-20K) | [Link](https://virutalbuy-public.oss-cn-hangzhou.aliyuncs.com/share/aigc3d/data/for_yisheng/LAM/LAM_20K.tar)   | 1.4 s               | 562.9FPS                    | 110+FPS   |
| LAM-20K | Our large dataset | TBD      | TBD      | 1.4 s               | 562.9FPS                    | 110+FPS   |

(**A & R:** 驱动渲染 )

```bash
# 从HuggingFace下载
# 下载相关资产
huggingface-cli download 3DAIGC/LAM-assets --local-dir ./tmp
tar -xf ./tmp/LAM_human_model.tar && rm ./tmp/LAM_human_model.tar
tar -xf ./tmp/LAM_assets.tar && rm ./tmp/LAM_assets.tar
huggingface-cli download yuandong513/flametracking_model --local-dir ./tmp/
tar -xf ./tmp/pretrain_model.tar && rm -r ./tmp/
# 下载模型权重
huggingface-cli download 3DAIGC/LAM-20K --local-dir ./exps/releases/lam/lam-20k/step_045500/


# 或者从OSS下载 (如果你无法从HuggingFace下载)
# 下载相关资产
wget https://virutalbuy-public.oss-cn-hangzhou.aliyuncs.com/share/aigc3d/data/LAM/LAM_assets.tar
tar -xf LAM_assets.tar && rm LAM_assets.tar
wget https://virutalbuy-public.oss-cn-hangzhou.aliyuncs.com/share/aigc3d/data/LAM/LAM_human_model.tar
tar -xf LAM_human_model.tar && rm LAM_human_model.tar
wget https://virutalbuy-public.oss-cn-hangzhou.aliyuncs.com/share/aigc3d/data/LAM/tracking_pretrain_model.tar
tar -xf tracking_pretrain_model.tar && rm tracking_pretrain_model.tar
# 下载模型权重
wget https://virutalbuy-public.oss-cn-hangzhou.aliyuncs.com/share/aigc3d/data/LAM/LAM_20K.tar
tar -xf LAM_20K.tar && rm LAM_20K.tar
```


### 运行Gradio
```
python app_lam.py
```

### 推理
```bash
sh ./scripts/inference.sh ${CONFIG} ${MODEL_NAME} ${IMAGE_PATH_OR_FOLDER} ${MOTION_SEQ}
```

### 致谢
本工作是建立在很多了不起的工作基础之上：

- [OpenLRM](https://github.com/3DTopia/OpenLRM)
- [GAGAvatar](https://github.com/xg-chu/GAGAvatar)
- [GaussianAvatars](https://github.com/ShenhanQian/GaussianAvatars)
- [VHAP](https://github.com/ShenhanQian/VHAP)

感谢他们对社区的杰出贡献。


### 更多工作
欢迎关注我们更多有趣的工作
- [LHM](https://github.com/aigc3d/LHM)


### 引用
```
@inproceedings{he2025LAM,
  title={LAM: Large Avatar Model for One-shot Animatable Gaussian Head},
  author={
    Yisheng He and Xiaodong Gu and Xiaodan Ye and Chao Xu and Zhengyi Zhao and Yuan Dong and Weihao Yuan and Zilong Dong and Liefeng Bo
  },
  booktitle={arXiv preprint arXiv:2502.17796},
  year={2025}
}
```
