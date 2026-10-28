<div align="center">

# toyauro-fleet

**Autonomous agent workbenches for a lights-out software factory.**

[English](README.md) · [简体中文](README.zh-CN.md)

</div>

ToyaUro Fleet brings independent agents and their existing tools together to
work across devices. A phone can run its own agents and tools; a Mac mini can
run its own. They collaborate as peers over existing connections such as SSH
and Tailscale. Humans set goals and can inspect or take over the work.

We start from tools agents can already use: tmux, shells, SSH and Git. Each
tmux panel is a general-purpose workbench; its name and responsibilities can
change with the task. Implement only the coordination that a real workflow
needs, and keep individual components useful on their own.

## Components

| Component | Purpose | Status |
| --- | --- | --- |
| [tmux-agent-adon](packages/tmux-agent-adon/) | Panel names, agent status lights and optional agent adapters. | Imported from the independent [tmux-agent-adon repository](https://github.com/toyauro/tmux-agent-adon). |
| Fleet communication | Discover panels and exchange requests and results through existing tmux and SSH. | Planned; not implemented or validated in this repository yet. |
| Software factory | Build and verify software using collaborating agents. | Direction for future real workflows; not yet implemented here. |

The independent adon repository remains available. Its MIT license and commit
history are preserved in the `packages/tmux-agent-adon` subtree. A clean clone of
this repository contains the component directly; no submodule is required.

## Try the status lights

From a shell inside the tmux server you want to use, after cloning this repo:

```sh
export PATH="$PWD/packages/tmux-agent-adon/bin:$PATH"
tmux run-shell "$PWD/packages/tmux-agent-adon/agent-adon.tmux"
```

Loading the plugin registers format fragments. To display them in the current
window, follow the [installation and display guide](packages/tmux-agent-adon/README.md#quick-start).
It describes how to integrate with an existing theme rather than replacing it.
The plugin can be used independently of the future fleet features.

## Current boundaries

- A status light reflects a report; it does not prove task completion or that
  the reporter is still alive.
- Panel discovery, cross-agent messaging, acknowledgments and automatic factory
  execution are goals to validate, not features already delivered.
- Device scopes remain autonomous; no central controller, database or broker
  is required by this repository today.

## License

The repository uses the [MIT License](LICENSE); component licenses remain in
their respective directories.
