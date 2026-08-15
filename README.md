# Smart Email Notifier

**ChatGPT-first AI 重要邮件智能提醒｜安装后告诉 ChatGPT 你不想错过什么，让它尽可能自动完成配置和后续提醒。**

[中文说明](./README.zh-CN.md) · [QQ Mail → Gmail → ChatGPT 示例](./docs/qqmail-gmail-chatgpt.md)

![QQ Mail → Gmail → ChatGPT privacy-safe demo](./assets/qqmail-gmail-chatgpt-demo.svg)

## 它解决什么问题？

重要邮件经常混在广告、Newsletter 和普通通知里。关键词过滤又不够聪明：真正重要的邮件可能只写“下一轮安排”，普通招聘宣传却可能同时出现“笔试、面试、测评”。

Smart Email Notifier 把两件事分开：

> **邮箱规则负责别漏掉，AI 负责别烦你。**

```text
邮件到达
  ↓
邮箱规则粗筛 / 必要时转发
  ↓
ChatGPT 可访问的邮箱
  ↓
AI 判断是否真的需要处理
  ↓
提取时间 / Deadline / 下一步动作
  ↓
只有重要事项才提醒
```

## 怎么用？

安装/提供 [`SKILL.md`](./SKILL.md) 后，直接告诉 ChatGPT 你的目标，例如：

```text
帮我配置秋招邮件提醒。
```

或者：

```text
帮我盯住所有需要我处理的学校通知。
```

Skill 会先检查当前 ChatGPT 能使用哪些能力。能直接完成的步骤应直接执行；只有登录、验证码、2FA、敏感授权或当前环境无法操作的邮箱设置才交给用户。

理想体验：

```text
告诉 ChatGPT 你不想错过什么
        ↓
检测邮箱 / Tasks / Browser 等能力
        ↓
能自动做的直接完成
        ↓
你只处理必要的登录 / 验证 / 授权
        ↓
以后自动检查并只提醒真正重要的邮件
```

> Skill 本身不会凭空获得邮箱或浏览器权限。实际自动化程度取决于当前 ChatGPT 环境已经提供并获授权的工具。

## 真实案例：秋招邮件提醒

这个 Skill 来自一个真实需求：招聘邮件主要进入 QQ 邮箱，但笔试、测评和面试通知很容易淹没在大量校招邮件中。

```text
QQ 邮箱
→ 新建「求职」文件夹
→ 收信规则粗筛
→ 自动转发 Gmail
→ ChatGPT 定时检查
→ AI 语义判断
→ 提醒真正需要完成的事项
```

QQ 邮箱首次配置可能需要本人完成手机号验证，Gmail 也可能需要本人确认转发。初始化完成后，邮件转发、AI 分类和定时检查可以持续自动运行。

详细脱敏教程见 [`docs/qqmail-gmail-chatgpt.md`](./docs/qqmail-gmail-chatgpt.md)，秋招策略见 [`presets/job-search-chatgpt.md`](./presets/job-search-chatgpt.md)。

## 还能用在哪？

- 求职：笔试、测评、面试、Offer、签约 Deadline
- 学校：考试、作业、行政通知、课程变更
- 账单：付款失败、续费、到期、退款异常
- 会议：邀请、改期、需要提前准备的事项
- 订单：配送异常、取件截止、退款状态
- 安全：异常登录、账号风险、需要本人确认的操作

场景只是 preset，核心逻辑不变：**先尽量召回，再由 AI 判断是否值得打扰你。**

## 仓库结构

```text
SKILL.md                       通用 Skill / 编排规则
CHATGPT.md                     ChatGPT-first 执行约定
presets/                       场景规则
 docs/qqmail-gmail-chatgpt.md  QQ 邮箱真实案例
assets/                        完全脱敏的公开演示素材
```

想了解自动化边界，可看 [`docs/automation-model.md`](./docs/automation-model.md)。普通用户不需要阅读其他设计文档即可使用。

## 隐私

公开截图和示例中不要出现真实邮箱、手机号、验证码、姓名、候选人/账号 ID、私人笔试或面试链接、会议链接、Token、Cookie、授权码、二维码或带身份参数的 URL。

仓库演示统一使用虚构数据，并明确标记：**演示数据 · 非真实招聘通知**。

## V1 范围

这是一个**通用 ChatGPT Skill**，不是独立邮箱软件，也不会绕过邮箱服务商的登录、2FA 或安全验证。它的目标是减少重复配置和人工翻邮箱，而不是绕过必要的安全步骤。

## License

No license has been selected yet.
