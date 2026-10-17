# X176 Freedom

**JamesDSP Liveprog 脚本** — 多级并行音频处理链

默认调音 **Warm Body**：去纸片感、保留体量、中性耐听。

---

## 功能概览

- **4 节点并行拓扑**（可独立配置 Mid / Side 权重）
- 参数均衡（SVF + Biquad）
- 动态塑形 / 谐波生成（odd / even / soft clip / wavefold 等）
- M/S 立体声场处理
- 可选空间与声音编辑总线（默认关闭，零额外开销）
- 条件旁通优化，未启用模块几乎不占用算力

默认 Warm Body 配置下估算约 **1.25k 单位/样本**，适合日常长时间使用。

---

## 兼容性

| 平台 | 状态 |
|------|------|
| JamesDSP（Android，含 RootlessJamesDSP） | 支持 |
| JDSP4Linux / JamesDSP for Linux | 支持 |

---

## 安装

1. 下载 [`X176_Freedom.eel`](X176_Freedom.eel)
2. 打开 JamesDSP → **Liveprog** → 导入脚本
3. 启用并按需微调

### 推荐微调旋钮

脚本内提供四个预增益旋钮（写在节点配置区）：

| 旋钮 | 作用 |
|------|------|
| `PRE_BASS` | 低频体量 |
| `PRE_BODY` | 低中频厚度 |
| `PRE_MID` | 中频 |
| `PRE_TOP` | 高频空气感 |

默认值 `1.0` = 原调音强度；设为 `0` 可关闭对应段。

---

## 默认调音说明（Warm Body v1）

目标：**把偏亮、偏薄、有纸片感的音频拉回自然**。

- **去纸**：3.3 kHz 钟形 −2.0 dB + 6.3 kHz 钟形 −1.2 dB
- **体量**：75 Hz 钟形 +1.8 dB + 250 Hz 低架 +1.0 dB
- **M/S**：低频节点只处理 Mid；去纸节点 Side 权重略高，侧声道中高多收一点
- **空间总线默认关闭**（避免反射抹糊瞬态，也节省大量算力）

空间相关 primitive（TAP / FDN / AIR 等）完整保留，需要时在脚本注释区有备份与示例。

---

## 文件说明

```
X176_Freedom.eel   主脚本（导入 Liveprog 使用）
LICENSE            MIT 许可证
README.md          本文件
```

---

## 版本

当前公开版本基于 **X176 Freedom 1.8.41 Warm Body Maintain**。

内部维护工具链（转译器、静态检查、性能热点分析等）不包含在本仓库中。

---

## 许可证

MIT License — 可自由使用、修改与分发。
