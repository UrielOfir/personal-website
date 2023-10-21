---
title: Creating a Keyboard Shortcut to Kill All User Processes
weight: 4
type: "docs"
description: >
  A guide on how to create a keyboard shortcut to quickly terminate all user processes on Ubuntu.
---

To quickly terminate all user processes in Ubuntu using a keyboard shortcut, follow these steps:

1. Verify in your terminal that this command is functioning correctly and effectively terminating all user processes:
   ```bash
   gnome-terminal -- bash -c "ps -U <user-name> -o pid= | xargs -I {} kill -9 {}"
   ```
   Replace `<user-name>` with your actual username.

2. Add the command as a custom keyboard shortcut in Ubuntu. For detailed instructions, refer to the [Ubuntu documentation on setting keyboard shortcuts](https://help.ubuntu.com/stable/ubuntu-help/keyboard-shortcuts-set.html.en).

This keyboard shortcut is invaluable when your operating system becomes unresponsive, as it allows you to avoid restarting your computer. Make sure to customize the keyboard shortcut according to your preferences.