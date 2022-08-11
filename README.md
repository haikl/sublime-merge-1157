This is a demo repo for reproducing https://github.com/sublimehq/sublime_merge/issues/1157

# Steps to reproduce

Option 1:
* open Sublime Merge
* in your favorite editor, create a new file `lfs/test1.lfs`, put some text in it, and save it
* go to Sublime Merge, and go to the Untracked Files section

Expected result:
* `lfs/test1.lfs` shows up in the list along with its content

Actual result:
* `lfs/test1.lfs` shows up in the list with a spinner running indefinitely
* open Task Manager and look for running git processes. There will be two: `git-lfs clean -- lfs/test1.lfs` and `git.exe clean -- lfs/test1.lfs`
* in Sublime Merge: try to close the repo. SM will lock up
* in Sublime Merge: close SM. The Window will vanish, but the process is still around (check Task Manager) and SM will not start again

Option 2:
* open Sublime Merge
* in your favorite editor, edit the file `lfs/test.lfs`, and save it
* go to Sublime Merge


# My config

* Windows 10 Enterprise N 19044.1826
* git version 2.37.1.windows.1
* git-lfs/3.2.0 (GitHub; windows amd64; go 1.18.2)
* Sublime Merge Build 2074
