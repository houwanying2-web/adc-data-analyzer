# ADC Data Analyzer

A lightweight Windows tool for ADC / STM32 / FPGA signal data analysis.

一个用于快速分析 ADC、STM32、FPGA 和示波器采样数据的 Windows 桌面工具。

> 当前版本：v0.1 Beta  
> 支持平台：Windows x64

---

## 下载

👉 [下载 ADC Data Analyzer v0.1 Beta](https://github.com/houwanying2-web/adc-data-analyzer/releases/tag/v0.1-beta)

下载 `ADC_Data_Analyzer.zip` 后：

1. 解压 ZIP
2. 打开 `ADC_Data_Analyzer` 文件夹
3. 双击 `ADC_Data_Analyzer.exe`

无需安装 Python。

> 当前 Beta 尚未进行数字签名，Windows 首次运行时可能提示“未知发布者”。

---

## 功能

目前支持：

- CSV / TXT 数据导入
- 拖拽打开数据文件
- 时域波形显示
- FFT 频谱分析
- 基波频率检测
- RMS
- SNR
- THD
- SINAD
- SFDR
- ENOB
- DC Offset 检测
- Clipping 检测
- Harmonic Distortion 检测
- Spectrum Leakage 提示

---

## 适合哪些数据？

例如：

- STM32 ADC 采样数据
- FPGA + ADC 采样数据
- 示波器导出的 CSV
- MCU 数据采集结果
- 其他等间隔采样信号

使用流程：

```text
导入 CSV / TXT
      ↓
输入采样率 fs
      ↓
点击 Analyze
      ↓
查看时域、FFT 和动态性能指标
```

这样可以减少为了查看一组采样数据，反复编写 MATLAB / Python FFT 分析脚本的工作。

---

## 支持的数据格式

当前支持：

```text
.csv
.txt
```

例如单列数据：

```text
0.124
0.235
0.318
0.412
```

或者：

```text
time,value
0.000001,0.124
0.000002,0.235
0.000003,0.318
```

支持常见逗号、空格和 Tab 分隔格式。

---

## 输出指标

### SNR

Signal-to-Noise Ratio，信噪比。

计算时会排除 DC、基波以及识别到的谐波功率。

### THD

Total Harmonic Distortion，总谐波失真。

用于衡量高次谐波相对于基波的总失真程度。

### SINAD

Signal-to-Noise-and-Distortion Ratio，信号与噪声失真比。

同时考虑噪声和谐波失真。

### SFDR

Spurious-Free Dynamic Range，无杂散动态范围。

表示基波与最大杂散成分之间的动态范围。

### ENOB

Effective Number of Bits，有效位数。

采用常见估算关系：

```text
ENOB = (SINAD - 1.76) / 6.02
```

该指标在接近满量程正弦输入条件下更具有代表性。

---

## 基础诊断

当前版本包含一些确定性规则，用于帮助快速发现常见问题，例如：

- 明显 DC Offset
- 波形削顶
- 明显二次 / 三次谐波
- 频谱泄漏迹象

例如：

```text
检测到明显谐波失真。

当前性能可能受到前端非线性、
输入幅度或 ADC 非线性的影响。
```

诊断仅用于辅助分析。

软件不会仅根据频谱直接认定具体硬件故障原因。

---

## Beta 说明

ADC Data Analyzer v0.1 Beta 当前定位为：

**工程快速分析 / 学习 / 实验辅助工具**

目前不是计量级 ADC 测试软件。

对于以下情况，需要谨慎解释测试结果：

- 极高动态范围测试
- 非相干采样下的极低噪声测量
- 信号非常接近 DC
- 信号非常接近 Nyquist Frequency
- 多个 Tone 距离非常接近
- 对 ADC Characterization 有严格测试规范要求

正式器件性能测试请同时参考：

- ADC Datasheet
- 芯片厂商推荐测试方法
- 专业测试仪器结果

---

## 当前已验证

v0.1 Beta 已通过合成测试数据验证，包括：

- 相干纯正弦
- 非相干纯正弦
- 约 40 dB SNR 的正弦 + 白噪声
- H2 = -40 dBc / H3 = -50 dBc 谐波测试
- Clipping 测试
- Spectrum Leakage 测试
- Harmonic Folding 测试
- 非相干 Spur SFDR 测试

自动化测试当前全部通过。

---

## Beta 测试

这是第一个公开 Beta 版本。

目前尤其希望获得更多真实数据进行测试，例如：

- STM32 ADC 数据
- FPGA 采样数据
- ADC 评估板数据
- 示波器 CSV
- 各种实际实验采样数据

如果你遇到：

- 文件无法读取
- 软件崩溃
- 指标明显异常
- 某种 CSV / TXT 格式无法识别
- 某个功能特别希望加入

欢迎提交 GitHub Issue。

真实使用反馈会决定后续版本优先开发哪些功能。

---

## Planned Improvements

后续是否加入以下功能，会根据 Beta 用户反馈决定：

- BIN / Raw ADC Data
- 自动报告导出
- 更多窗函数
- 批处理
- 更强的高动态范围分析
- 更多 ADC 测试模式
- 更灵活的数据列选择
- 更多示波器文件格式兼容

不会为了堆功能而盲目开发。

---

## Version

### v0.1 Beta

First public beta release.

包含：

- Windows x64
- CSV / TXT Import
- Time-domain Analysis
- FFT Spectrum
- Fundamental Detection
- RMS
- SNR
- THD
- SINAD
- SFDR
- ENOB
- Basic Signal Diagnostics

---

## Feedback

如果这个工具对你的 STM32 / FPGA / ADC 项目有帮助：

⭐ 欢迎 Star this repository

也欢迎通过 GitHub Issue 告诉我：

**你最希望下一版增加什么功能？**

---

## Disclaimer

ADC Data Analyzer 当前仍处于 Beta 阶段。

本工具主要用于工程分析、学习和实验辅助，不应作为计量级测试结果或器件最终性能认证依据。

对于正式 ADC 性能评估，请结合芯片厂商推荐测试方法、Datasheet 和专业测试设备进行验证。
