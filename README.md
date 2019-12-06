# vscode-terminal-bug

Demo project demonstrating a bug in vscode where Windows conhost processes for build tasks are not terminated when the "terminate build task" command is run. (alternatively, can be seen as a bug of the build tasks not reusing existing conhost instances, if they're meant to be re-used)

### Reproduction instructions

1) Clone this repo.

2) Open the repo's root folder in VSCode.

3) Press Help -> Open Process Explorer, and leave the window open to the side (so you can see the phantom conhost processes).

4) Run the "Tasks: Run Build Task" command, and select one of the two "build tasks" (they're just endless echo loops). You'll see new processes in the process-explorer.

5) Run the "Tasks: Terminate Task" command, and "terminate" the just-started task. The process-count will not go down, I suppose because vscode is trying to reuse the terminal processes, as per the message "Terminal will be reused by tasks, press any key to close it." when terminating using ctrl+c manually.

6) However, if you run the "Tasks: Run Build Task" command again, the old conhost processes does *not* get reused. Instead, it just stays around as a phantom process.

7) If you terminate the second build task, and start it again, yet another instance of conhost starts, with none of the old conhosts getting removed/reused. And so on, for every new launch of a build task.

### Screen capture

Here is a screen capture of me performing the steps above on a fresh clone of this repo:
![](TODO)

### Why this is a problem

To see why this is a problem, see the rest of my issue report here: [TODO: link to issue]