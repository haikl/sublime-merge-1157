# Build 2081 fixes the issue. Thanks, Sublime Team!

This is a demo repo for reproducing https://github.com/sublimehq/sublime_merge/issues/1157

# Steps to reproduce

## Option 1
* have a clean repo
* open Sublime Merge (should show no changes and an empty summary page)
* in your favorite editor, create a new file `lfs/new.lfs`, put some text in it, and save it
* go to Sublime Merge, and go to the Untracked Files section

Expected result:
* `lfs/new.lfs` shows up in the list along with its content

Actual result:
* `lfs/new.lfs` shows up in the list with a spinner running indefinitely
* the UI is still responsive, you can check other commits, work with other repos, change preferences etc.
* open Task Manager and look for running git processes. There will be two: `git-lfs clean -- lfs/new.lfs` and `git.exe clean -- lfs/new.lfs`
* in Sublime Merge: try to close the repo. SM will lock up
* in Sublime Merge: close SM. The Window will vanish, but the process is still around (check Task Manager) and SM will not start again

## Option 2
* have a clean repo
* open Sublime Merge (should show no changes and an empty summary page)
* in your favorite editor, edit the file `lfs/test.lfs`, and save it
* go to Sublime Merge, and go to the current changes

Expected result:
* `lfs/test.lfs` shows up in the summary along with its changes
* `lfs/test.lfs` shows up as a separate tab

Actual result:
* nothing shows up (SM still shows "No changes") 
* the UI is still responsive, you can check other commits, work with other repos, change preferences etc.
* open Task Manager and look for running git processes. There will be two: `git-lfs clean -- lfs/test.lfs` and `git.exe clean -- lfs/test.lfs`
* in Sublime Merge: try to close the repo. SM will lock up
* in Sublime Merge: close SM. The Window will vanish, but the process is still around (check Task Manager) and SM will not start again


# My config

* Windows 10 Enterprise N 19044.1826
* git version 2.37.1.windows.1 (installed from https://gitforwindows.org/)
* git-lfs/3.2.0 (GitHub; windows amd64; go 1.18.2)
* Sublime Merge Build 2074. It is configured to system Git binaries. Using the bundled git has no impact, it still seems to use the system git-lfs and hangs
