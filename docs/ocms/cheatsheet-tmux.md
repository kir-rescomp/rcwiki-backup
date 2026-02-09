---
title: Cheatsheet tmux
description: Tips for using tmux sessions
published: true
date: 2024-05-22T15:05:47.472Z
tags: tmux, cheatsheet
editor: markdown
dateCreated: 2024-05-22T15:05:35.655Z
---

-U# Cheat Sheet: Tmux

This page contains helpful tips for using Tmux. This includes how to activate and deactivate Tmux sessions and make use make use use of panes and windows.

## Session
`tmux attach` attach previous session

`ctrl b d` detach current session. tmux session keeps running.

## Copy mode
`ctrl b [` Enter copy mode. can use up, down, PgUp, PgDn arrows to scroll through the console. `q` to exit mode.

`ctrl b PgUp` Enter copy mode and scroll one page up. `q` to exit mode

## Panes
`ctrl b "` Split pane horizontally so you get a new pane below current pane

`ctrl b %` Split pane vertically so you get a new pane beside current pane

`ctrl b left-arrow` Navigate to pane to the left. Can use up, down, left, right arrows.

`ctrl b x` Close current pane

`ctrl b :resize-pane -L 10` Resize current pane. Use `D, U, L, R` flags to determine direction of size increase. Can optionally specify number of cells to increase by.

`ctrl b :break-pane` Breaks out current pane into a new window

`ctrl b {` swap panes; `{` moves to the left; `}` moves to the right

## Windows
`ctrl b c` new window

`ctrl b n` move to next window


