# 阅读工作区 Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [x]`) syntax for tracking.

**Goal:** 创建以授课和严格掌握制为核心、可跨会话接续的本地阅读工作区。

**Architecture:** AGENTS.md 是导师规则的唯一来源，CLAUDE.md 通过 @AGENTS.md 引用。每本书在 library 下保存原始教材、课程、进度和正式测验记录。

**Tech Stack:** Markdown、本地 PDF；不开发应用或脚本，不安装依赖。

## Global Constraints

- 以中文或英文交流。
- 不编造教材内容、学习目标、课纲、回答或通过记录。
- 每本书先确认目的、基础和深度，课纲确认后授课。
- 所有必达目标独立达标才能通过；提示下完成的回答不算正式通过。
- 不初始化 Git、不创建提交、不进行远端操作。

### Task 1: 导师规则与入口

**Files:** Create `AGENTS.md`, `CLAUDE.md`.

**Interfaces:** CLAUDE.md 引用根目录 AGENTS.md；规则定义新书登记、教材检查、课纲确认、授课、测验和保存流程。

- [x] 创建规则，覆盖来源区分、材料不全、逐题测验、目标级通过判定、补讲复测、复习和跨会话恢复。
- [x] 创建 CLAUDE.md，内容为 `@AGENTS.md`。
- [x] 检查引用存在且所有上述流程明确。

### Task 2: 首本书档案

**Files:** Move 根目录现有 PDF to `library/如何快速了解一个行业/source/`，保留原文件名；Create `course.md`, `progress.md`, `assessments.md` in `library/如何快速了解一个行业/`.

**Interfaces:** course.md 提供目标、教材状态、课纲与通过标准；progress.md 提供恢复位置和目标级状态；assessments.md 提供测验依据。

- [x] 记录 PDF 已提供但未成功读取，目标未确认、课纲未生成、尚未授课与测验。
- [x] 移动教材，不覆盖同名文件。
- [x] 检查 PDF 哈希在移动前后相同，根目录不再有原文件。
- [x] 独立验证所有文件、引用、初始状态及教学规则；通过后复跑验证中的文件检查命令。

## 验收边界

结构与规则可以通过文件检查及情景审阅验证；实际教学闭环与新会话接续需要用户确认目标并进行学习后验证，不宣称已完成。
