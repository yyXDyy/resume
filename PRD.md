# 杨翔皓个人展示页 PRD

## 1. Executive Summary

**Problem Statement：** 当前 PDF 简历信息完整，但内容密度较高，招聘方在短时间内不容易看出候选人的能力脉络。页面需要呈现一条从测试基本功到云平台质量保障、自动化、Kubernetes 排障、AI 辅助测试和测试左移的成长路径。

**Proposed Solution：** 在 `resume/` 项目中构建一个可静态部署的个人展示页。页面采用“个人座右铭 + 成长路径 + 当前高点 + 成长痕迹档案 + 下一阶段想补的能力”的结构：首屏突出“质量是被设计出来的”，后续用 Q1 OKR 中的测试体系改进、前置沟通、自动化回归和测试左移实践说明能力如何落地。

**Success Criteria：**

- 首屏 10 秒内能看清候选人定位和座右铭：质量是被设计出来的。
- 首屏必须展示 4 个关键量化成果：6000+ 用例/检查项、900+ 缺陷、2.4h 回归耗时、40% 效率提升。
- 页面必须包含“成长路径”模块，说明候选人从测试执行、云平台质量、自动化工具、Kubernetes 排障到测试左移的能力递进。
- 页面必须包含“当前高点”表达，说明 2026 Q1 开始从被动发现 Bug 转向系统性预防和需求阶段提前介入。
- 页面必须包含“接下来想补上的部分”，说明候选人希望继续提升发布流程、自动化稳定性、云原生排障和团队质量推进经验。
- 页面必须包含“成长痕迹档案”模块，每个档案条目说明：对应的成长阶段、实现方式、可展示材料、产生价值。
- 页面应在桌面端 1440px 与移动端 390px 宽度下无文字重叠、无横向滚动。
- 静态页面可直接用于 GitHub Pages、Sealos 静态站点或其他静态托管。

## 2. User Experience & Functionality

### User Personas

- **HR / 招聘专员：** 需要快速判断候选人的方向、技术关键词、薪资区间匹配度和是否值得约面。
- **测试负责人 / 技术面试官：** 关注候选人是否具备真实测试设计、测试开发、云平台排障、缺陷复盘和自动化落地能力。
- **候选人本人：** 需要一个比 PDF 简历更适合公开分享的展示入口，用来承接 Boss 直聘、GitHub、投递开场白和面试前资料补充。

### User Stories

- **As a HR,** I want to quickly see the candidate's role positioning, core skills and achievement metrics so that I can decide whether to invite them to interview.
- **As a QA lead,** I want to inspect project details, implementation methods and evidence artifacts so that I can judge whether the experience is real and relevant.
- **As the candidate,** I want to share one clean portfolio URL so that recruiters can understand my work beyond a PDF attachment.

### Acceptance Criteria

- 首屏不展示个人头像，避免页面变成普通求职资料卡。
- 首屏包含姓名、定位、座右铭、成长说明、关键指标和主要 CTA。
- 页面包含固定信息结构：个人座右铭、成长路径、下一阶段想补的能力、专业技能、Sealos 工作经历、成长痕迹档案、代表项目、联系入口。
- 成长痕迹档案至少包含 4 类：
  - CronJob 用例矩阵：展示 242 条用例如何转为 Playwright 测试矩阵。
  - AppStore 批量验证：展示模板批量创建、Ready 判断、失败信息和清理能力。
  - Kubernetes 排障：展示 UI 验证与 Pod/Service/log/kubectl 状态检查结合。
  - Test Skill 与测试左移：展示任务识别、truth model、需求澄清、blocker 判断、测试/诊断工件和可执行测试沉淀。
- 每个项目/档案条目必须回答 3 个问题：这个阶段有什么变化、做了什么、产生什么价值。
- 页面视觉风格专业、克制、可信；不使用大面积装饰性渐变、漂浮卡片堆叠或夸张营销文案。
- 移动端首屏应优先显示姓名、定位、核心 CTA 和关键指标；导航不应占用过多高度。
- 页面应包含下载 PDF 简历入口，默认链接到 `assets/cv-comprehensive-quality-engineer-compact-a4.pdf`。

### Non-Goals

- 不做博客系统、登录系统、后台管理或动态 CMS。
- 不做复杂动画、3D 效果或重营销落地页。
- 不展示敏感工单详情、私有仓库内部数据、账号信息、客户隐私、未脱敏截图或内部飞书链接。
- 不直接复制 5 页详细简历全文，页面应优先展示结构化摘要和可信工作痕迹。

## 3. AI System Requirements

本项目展示页本身不需要接入 AI 功能。AI 相关内容仅作为候选人的项目能力展示：

- 展示 Customer Advocate Agent 的工作流设计能力。
- 说明 AI 辅助测试用于需求拆解、风险分析、用例生成、可执行性审查和交付审计。
- 明确“AI 负责语义判断、脚本负责机械校验”的质量边界。
- 对外呈现时避免暗示 AI 已自动完成所有测试，只说明其在测试设计、过程整理、脚本规划和 SOP 沉淀中的辅助价值。

## 4. Technical Specifications

### Architecture Overview

MVP 采用纯静态页面：

```text
resume/
  PRD.md
  index.html
  README.md
  assets/
    cv-comprehensive-quality-engineer-compact-a4.pdf
  output/
    sample-desktop.png
    sample-mobile.png
    reference-abdussalam-desktop.png
```

页面结构：

- `Hero`：姓名、定位、座右铭、成长说明、CTA、关键指标。
- `Growth Path`：测试基本功、云平台复杂度、自动化工具化、测试左移。
- `Current Peak`：Q1 测试体系改进，回归效率提升 40%，需求阶段提前介入，开始从“围着 Bug 转”走向“站在 Bug 之上”。
- `Next Step`：下一阶段想补质量门禁、自动化稳定性、云原生排障和团队质量推进经验。
- `Skill Overview`：测试设计、云平台排障、自动化、AI 测试、接口/性能、协作管理。
- `Work Experience`：Sealos 工作内容与代表成果。
- `Growth Traces`：成长留下的工作痕迹，参考 `abdussalam.pk/behind-the-scenes` 的过程档案表达方式，重点展示测试左移、自动化和云原生排障相关材料。
- `Projects`：Sealos 自动化质量工具链、Customer Advocate Agent、Monitor-Test。
- `Contact`：只保留姓名、城市、手机号和邮箱；手机号与邮箱点击即复制，不跳转；不出现“岗位机会”“方向匹配”等求职提示语。

### Reference Inspiration

参考页面 `https://abdussalam.pk/behind-the-scenes` 的可借鉴点：

- 轻导航，减少首屏噪音。
- 大标题 + 短说明，先建立页面主题。
- 用“过程档案”展示能力，而不是只罗列最终项目名称。
- 每个档案条目用大幅过程材料承载可信度，例如图表、草稿、流程、报告、矩阵或截图。
- 内容保持克制，强调真实工作痕迹。

本项目的转译方式：

- 将 “Behind the Scenes” 转为 “成长留下的痕迹 / Growth Traces”。
- 将设计过程图替换为测试资产：用例矩阵、自动化报告、Kubernetes 检查面板、AI 测试流程图、负载场景曲线。
- 不复制参考站点的视觉语言，保留测试开发、云平台、质量工程的专业气质，并突出个人成长线。

### Content Model

```text
ProofItem {
  category: string        // CASE MATRIX / AUTOMATION / K8S DEBUG / LEFT SHIFT
  title: string           // 档案标题
  growth: string          // 对应的成长阶段
  problem: string         // 当时遇到的问题
  action: string          // 实现方式
  trace: string           // 可展示材料或工作痕迹
  value: string           // 产生的价值
  link?: string           // 项目或 GitHub 链接
  artifactType: string    // matrix | report | terminal | workflow | chart
}
```

### Integration Points

- GitHub：`https://github.com/yyXDyy`
- Sealos 展示链接：`https://hzh.sealos.run`
- 项目展示：
  - Sealos 自动化质量工具链：仓库记录可能包含私有内容，页面不直接放仓库链接，改为“私有记录 · 可提供脱敏说明”。
  - Customer Advocate Agent：如果仓库仍为私有，页面不直接放仓库链接，改为“私有项目 · 可提供脱敏演示”。
  - Monitor-Test：公开仓库可保留链接 `https://github.com/yyXDyy/Monitor-Test`。
- PDF 简历：`assets/cv-comprehensive-quality-engineer-compact-a4.pdf`

### Security & Privacy

- 公开站点不展示未脱敏内部截图、客户信息、工单原文、飞书内部链接、密钥、账号和集群敏感信息。
- 私有仓库只展示项目名称、问题背景、方法论、脱敏指标和可提供脱敏说明，不在公开页面暴露仓库地址。
- 页面公开展示手机号和邮箱，结尾只说明联系渠道；手机号与邮箱点击即复制，如后续需要降低公开暴露程度，可改为图片化或表单入口。
- GitHub Pages 部署前需检查所有链接和资源是否适合公开访问。

## 5. UI / Layout Requirements

### Visual Direction

- **整体气质：** 专业、清晰、技术可信，有质量工程和云平台工具感。
- **参考方向：** 借鉴参考站的“过程档案”叙事，而不是做传统卡片堆叠式简历。
- **页面密度：** 首屏高效，项目区适度展开；避免长段落连续堆叠。
- **色彩：** 白底、深墨色文本、灰色分割线，辅以红色小标题、蓝色链接和绿色状态点；避免单一蓝紫渐变。
- **卡片：** 仅用于指标、技能组和痕迹条目；边框半径不超过 8px。
- **排版：** 标题明确，正文可扫读；数字指标突出但不浮夸。

### First View Layout

桌面端：

- 顶部轻导航：Logo/姓名 + 成长/技能/痕迹锚点 + 下载简历。
- 左侧为座右铭大标题、定位、成长简介和 CTA。
- 右侧为座右铭解释、求职方向摘要和关键指标，不展示头像。
- 首屏底部露出“成长路径”开头，提示继续浏览。
- 首屏文案需要带出开放心态：已有真实经验，但仍希望继续补发布流程、自动化稳定性和质量推进能力。

移动端：

- 导航压缩为简短横向链接或隐藏次要链接。
- 指标改为 2 列或单列。
- CTA 纵向排列，按钮高度固定。
- 痕迹档案改为单列，过程图模拟块置于文字下方。

### Artifact Preview Rules

- 用 CSS 绘制样例矩阵、报告、终端日志、流程图和曲线，作为视觉样例，不使用未经授权的内部截图。
- 每个视觉块要像真实工作产物：有表头、状态、命令、检查项、失败信息或阶段名称。
- 不把视觉块做成纯装饰；它必须对应候选人的某项能力。
- 对公开页面，视觉块中的命名使用脱敏或通用表达。

## 6. Risks & Roadmap

### Risks

- **内容过长：** 候选人经历丰富，直接铺满会降低浏览效率。MVP 应优先展示摘要、痕迹档案和项目链接。
- **私有仓库不可访问：** 部分仓库可能是私有或权限受限，应给出“可提供脱敏说明/可提供脱敏演示”的替代描述。
- **数字可信度：** 所有量化数据应与简历、OKR 或测试记录一致，避免超过可追溯范围。
- **移动端拥挤：** 技能标签、指标和过程图需要响应式换行，避免横向滚动。
- **过度包装：** 页面要展示价值，但不能显得像包装过度；应坚持“问题、行动、结果、痕迹”的表达。

### Phased Rollout

- **MVP：** 单页静态 HTML，包含完整信息架构、视觉样例、成长痕迹档案和 PDF 下载入口。
- **v1.1：** 加入项目详情锚点、脱敏截图墙、简历下载统计和移动端导航优化。
- **v2.0：** 部署到 GitHub Pages 或 Sealos，补充英文版、项目 Demo、交互式技能过滤和更多可公开过程材料。

## 待确认问题

1. 展示页是否公开手机号，还是改成邮箱、微信二维码或“点击复制联系方式”？
2. 正式部署前确认手机号和邮箱是否继续公开；页面本身不展示头像。
3. 页面最终更偏“求职投递页”还是“技术作品集页”？如果偏投递页，首屏更短；如果偏作品集，成长痕迹可以更展开。
4. 是否允许后续加入脱敏后的飞书用例截图、issue 截图和自动化运行报告截图？
