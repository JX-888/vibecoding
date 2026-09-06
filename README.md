# 虚拟用户测评平台 Demo

基于「虚拟用户测评平台 Demo PRD」实现的可交互 Demo，单文件 HTML（无外部依赖），用于演示「上传数据 → 生成虚拟用户 → 对话测试 → 测评报告」三页主流程。

## 文件结构

```
virtual-user-demo/
├── index.html               # 主 demo，单文件（CSS / JS / 数据均内嵌）
├── README.md                # 本说明
└── screenshots/             # 各阶段 UI 截图（10 张）
    ├── 01_page1_init.png
    ├── 02_page1_uploaded.png
    ├── 03_page1_generating.png
    ├── 04_page1_generated.png
    ├── 04b_page1_api_connected.png
    ├── 05_page1_ready.png
    ├── 05_page1_ready_full.png
    ├── 06_page2_started.png
    ├── 07_page2_mid.png
    ├── 08_page2_done.png
    ├── 09_report_top.png
    └── 10_report_mid.png
```

## 怎么打开

直接双击 `index.html` 即可在浏览器中打开。所有逻辑都在一个文件里，不需要构建步骤。

建议浏览器：Chrome / Edge / Safari 最新版。

## 怎么跑通整个流程

Demo 默认是「未初始化」状态，按以下顺序操作即可走完全流程：

### 第一步：上传数据（页面一）

1. 在 **「1. 数据上传」** 模块依次点击 5 个上传卡片（基础身份 / App 足迹 / 聊天记录 / 录音 / 备注），点开后点「确认上传模拟数据」
2. **「2. Agent API 接入」**：点「测试连接」，模拟 API 校验
3. **「3. 业务目标设定」**：选一个目标（默认即可）
4. **「4. 生成虚拟用户」**：点「开始生成」，等待进度条走完
5. 进度完成后按钮变成「**开始对话测试**」

### 第二步：对话测试（页面二）

- 默认进入页面二，左侧是虚拟用户列表，右侧是默认选中第一个用户的微信式聊天窗
- 点左侧其他用户可切换聊天上下文
- 顶部「**列表视图 / 网格视图**」可切换用户一览
- 底部「开始对话测试」按钮触发所有用户并行对话
- 对话完成后所有用户进入「已完成」状态，可点进任一用户看完整对话

### 第三步：测评报告（页面三）

- 对话全部完成后，「**生成报告**」按钮亮起
- 点生成后跳转到页面三：综合得分环、结束状态分布、7 维度得分、虚拟用户一览
- 顶部可切换「V1 当前版本 / V2 优化版本」对比得分差异

## Demo 内置的参考数据资产（只读查看）

- 点击页面顶部的「**字段模板库 / 画像标签体系 / 测评指标体系**」按钮可弹出只读模态框，查看完整定义

## 实现说明（给后续接手者的笔记）

- **单文件**：所有 HTML / CSS / JS / 模拟数据都内嵌在 `index.html`，没有外部依赖
- **状态机**：`let state = {uploaded, connOk, usersGenerated, testing, allDone, speed, version, chatUid}`
- **页面切换**：`.page.active` 控制显示，CSS transition 300ms
- **聊天节奏**：MVP 阶段统一固定节奏（默认 1200ms / 加速 350ms），不按画像区分思考时长
- **结束判定**：由各虚拟用户性格触发达成 / 观望 / 顾虑 / 沉默 / 拒绝 / 人工六种结束状态
- **20 个 mock 虚拟用户**写在 `USERS` 数组，含 id / name / role / tags / 画像 / 对话 / 结束状态
- **V1/V2 对比**：报告页可切换两个版本的得分，用于演示「V1 测评 → 优化 Agent → V2 复测」闭环

## 关联 PRD

- Feishu PRD 文档：https://guanghe.feishu.cn/docx/IVKWdX7SaoZ40zxcaoqcHaBinDg
- 原始 Demo PRD：https://guanghe.feishu.cn/wiki/ZWsAwwwvcihOpvkOJVIcdfGxnq2

## 版本

V1.0（2026-09-06）
