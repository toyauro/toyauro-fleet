<div align="center">

# toyauro-fleet

**为黑灯软件工厂打造自主的 Agent 工位。**

[English](README.md) · [简体中文](README.zh-CN.md)

</div>

ToyaUro Fleet 让跨设备的独立 Agent 与现有工具协作：手机运行自己的 Agent 和手机工具，Mac mini 运行自己的 Agent；双方通过 SSH、Tailscale 等现有连接平等通信。人提出目标，也可以随时查看和接手工作。

我们从 Agent 已经会用的工具开始：tmux、Shell、SSH 和 Git。每个 tmux panel 都是一个通用工位，名称和职责可以随任务改变。只在真实工作流需要时补充必要的协作能力，并让各组件能够独立使用。

## 组件

| 组件 | 用途 | 当前状态 |
| --- | --- | --- |
| [tmux-agent-adon](packages/tmux-agent-adon/) | panel 名称、Agent 状态灯和可选适配器。 | 已从[独立 adon 仓库](https://github.com/toyauro/tmux-agent-adon)导入。 |
| Fleet 通信 | 发现 panel，复用 tmux 和 SSH 交换请求与结果。 | 规划中；本仓库尚未实现或验收。 |
| 软件工厂 | 让协作的 Agent 构建和验证软件。 | 未来以真实任务驱动，尚未在本仓库实现。 |

独立 adon 仓库继续保留；其 MIT 许可证和提交历史保留在 `packages/tmux-agent-adon` 子树中。克隆本仓库即可获得组件源码，不需要初始化 Git submodule。

## 试用状态灯

克隆本仓库后，在目标 tmux server 的 shell 中执行：

```sh
export PATH="$PWD/packages/tmux-agent-adon/bin:$PATH"
tmux run-shell "$PWD/packages/tmux-agent-adon/agent-adon.tmux"
```

加载插件会注册显示格式。要在当前窗口显示灯，请继续查看[安装与显示指南](packages/tmux-agent-adon/README.zh-CN.md#快速开始)，其中也说明了如何保留已有主题。插件可以独立于未来的 fleet 通信使用。

## 当前边界

- 状态灯反映报告，不证明任务完成，也不保证报告方仍然存活。
- panel 发现、跨 Agent 消息、接收确认和自动化工厂执行仍待实现和验证。
- 各设备保持自主；本仓库目前不要求中心控制器、数据库或消息代理。

## 许可证

仓库使用 [MIT 许可证](LICENSE)，组件目录中保留各自许可证。
