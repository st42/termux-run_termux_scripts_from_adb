# termux-run_termux_scripts_from_adb
**Run Termux scripts from Android Debug Bridge**

If you want to run a Termux script from adb use one of the following methods:

**Method 1:**
This method will run the script regardless of whether a Termux shell is already running not. However you have to allow adb root access on your phone.
```
adb shell am startservice -n com.termux/com.termux.app.TermuxService -a com.termux.service_execute -d /data/data/com.termux/files/home/.shortcuts/script.sh
```
The -d option is the path/script-name that you want to run
The script doesnt have to be in the .shortcuts directory either

If you don't want to allow adb root access you can use the following:

**Method 2:**
```
adb shell am start -n com.termux/com.termux.app.TermuxActivity
adb shell input text '/data/data/com.termux/files/home/.shortcuts/script.sh'
adb shell input keyevent 66
```
The 1st line opens a Termux shell
The 2nd line types in the path/script-name
The 3rd line presses the enter key

**Warning:** This method will bring to the forefront a Termux shell if one is currently running and use it. If it is not sitting at a waiting bash prompt, the script will not run. If you want to kill any running Termux shells to insure that the script runs use the following:
```
adb shell am force-stop com.termux
```
This will kill all running Termux shells and everything associated with it.

