---
title: "Fixing iTerm2"
layout: post
date: 2016-04-02 19:47
#tag: markdown
#star: true
---

For some reason iTerm2 doesn't exhibit typical \*nix behaviour for the alt-left, alt-right and alt-backspace keybindings. To fix this, head to iTerm > Preferences > Profiles > Keys and add the following keyboard shortcuts.

- alt + left -> Send Escape Sequence -> esc + b
- alt + right -> Send Escape Sequence -> esc + f
- alt + backspace -> Send Hex Code -> 0x17

Now you should be able to navigate as normal.
