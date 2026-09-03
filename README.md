# 个人介绍

**抖音博主**

**科研棱镜：** 全网粉丝 20w+，一起拥抱 AI 科研的无限可能！

- AI 集成站：[https://ai.hejingpt.com/](https://ai.hejingpt.com/)
- API 中转站：[https://api.sciprism.com/](https://api.sciprism.com/)
- 微信：`LN01678`

## Codex Skills

本仓库包含以下 Codex Skills：

- [`literature-to-mechanism-figure`](./literature-to-mechanism-figure)：从论文或研究材料中提取证据，生成机制图规划并调用图像生成能力制作科研机制图。
- [`research-text-to-figure`](./research-text-to-figure)：将用户提供的科研文本转换为证据约束的概念机制图。

每个 Skill 的详细使用说明请参阅对应目录中的 `SKILL.md`。

## 安装

直接把下面这句话发送给 Codex：

```yaml
请安装这个仓库中的全部 Codex Skills：
https://github.com/summer-ai-lab/sci-figure
```

Codex 会识别并安装仓库中的两个 Skill。安装完成后，新建一个任务即可使用。

## 1. 根据研究文字绘图

调用 `$research-text-to-figure`，并在请求中提供实际研究内容：

```text
使用 $research-text-to-figure

研究内容：
Vitamin D/VDR signaling induces miR-27a/b in oral lichen planus ...
```

还可以补充以下限制：

- 目标期刊或使用场景；
- 必须出现的分子、组织或细胞标签；
- 中文或英文标签；
- 指定配色和构图重点。

该 Skill 只把用户提供的文字作为事实来源，不会自行补充外部文献知识。如果文字没有支持完整机制，会改为生成概念总结图或结果流程图。

## 2. 根据论文绘图

调用 `$literature-to-mechanism-figure`，并提供论文标题、PDF 路径、DOI 或正式网址：

```text
使用 $literature-to-mechanism-figure

论文/PDF/DOI：
10.1021/acscatal.3c02613
```

本地 PDF 示例：

```text
使用 $literature-to-mechanism-figure

论文/PDF/DOI：
/absolute/path/to/paper.pdf
```

该 Skill 优先使用作者或出版社提供的摘要与结论，不会只凭论文标题或搜索结果摘要绘图。若无法取得摘要或结论，会要求用户提供 PDF 或粘贴原文。

## 两个 Skill 的区别

| Skill | 事实来源 | 适用场景 |
| --- | --- | --- |
| `research-text-to-figure` | 用户提供的研究文字 | 自己的实验总结、研究设想、摘要草稿、项目说明 |
| `literature-to-mechanism-figure` | 论文 Abstract 和/或 Conclusion | DOI、论文标题、期刊网址、本地 PDF、文献摘要 |

## 默认输出与证据规则

- 每次任务默认只生成一张最终图片。
- 默认画幅为 16:9，背景为纯白色。
- 默认采用从左到右的 3–6 阶段阅读路径。
- 英文来源默认使用英文科学标签。
- 关联关系不能升级为因果关系；不确定或假设关系应使用虚线或不确定性标记。
- 只有来源明确给出的关键数值才可以出现在图片中。
- 不得虚构分子、通路、细胞类型、剂量、时间点、样本量或实验结果。
- 如果来源只支持结果、不支持机制，应输出 graphical abstract 或结果路径图，而不是伪造机制图。

## 注意事项

- AI 生成图片可能出现标签拼写或局部箭头错误，正式投稿前仍需人工核对。
- “BioRender-inspired”表示采用简洁的科研插画语言，不包含或分发 BioRender 素材。
- 仓库中的 Skill 文件为英文版；本 README 使用中文说明安装及调用方式。
