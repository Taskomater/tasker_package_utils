# Tasker Package Utils

This is a project to provide some utils related to Tasker App package.

### Downloads
Download latest release from [here](https://github.com/Taskomater/Tasker-Package-Utils/releases).
##


### **`tasker_package_utils script:`**

You can run the script placed in the current directory without setting the ownership and permission by running the command `bash tasker_package_utils`.
If you are not running the script in termux, set the shebang of the script correctly (the first line of the script).

##### Usage:

```
Usage:
  tasker_package_utils [ -h | --help ]
  tasker_package_utils [ --version ]
  tasker_package_utils command [command_options]

Available commands:
  convert_system_priv     convert tasker user app to system privileged app
  convert_user            convert tasker system privileged app to user app
  uninstall               uninstall tasker
  perms                   manage tasker permissions


Use \"tasker_package_utils command [ -h | --help ]\" for more help about a command.
```
##


- **`tasker_package_utils convert_system_priv`**

##### Usage:

**`tasker_package_utils convert_system_priv`** command is used to convert tasker user app to system privileged app.

```
tasker_package_utils convert_system_priv command is used to convert tasker user app to system privileged app.


Usage:
  tasker_package_utils convert_system_priv [command_options] -d|n

Available command_options:
  [ -h | --help ]    display this help screen
  [ -v | -vv ]       set verbose level to 1 or 2
  [ -n ]             normal conversion mode
  [ -d ]             dirty conversion mode


If the 'n' option is passed, then normal conversion mode will be used and during conversion tasker will \
be uninstalled and you will loose all tasker data and desktop shortcuts.

If the 'd' option is passed, then dirty conversion mode will be used and during conversion tasker will \
not be uninstalled and you will not loose any tasker data or desktop shortcuts but this can leave the \
packages info of android system in an inconsistent state and you might have trouble uninstalling tasker \
later.

set verbose level to 1 or 2 to get more info when running tasker_package_utils names command.
```

##### Examples:

```
#Convert tasker user app to system privileged app in normal mode
#this will uninstall tasker and you will loose all tasker data and desktop shortcuts
bash tasker_package_utils convert_system_priv -n

#Convert tasker user app to system privileged app in dirty mode
#this will not uninstall tasker and you will not loose any tasker data or desktop shortcuts
#but this can leave the packages info of android system in an inconsistent state and you might have trouble uninstalling tasker
#you may need to manually remove tasker apk to uninstall and remove "net.dinglisch.android.taskerm" tags from "/data/system/packages.xml"
bash tasker_package_utils convert_system_priv -d
```
##


- **`tasker_package_utils convert_user`**

**`tasker_package_utils convert_user`** command is used to convert tasker system privileged app to user app.

**This is currently unsupported and will be implemented later.**

##### Usage:

```
tasker_package_utils convert_user command is used to convert tasker system privileged app to user app.


Usage:
  tasker_package_utils convert_user [command_options] -d|n

Available command_options:
  [ -h | --help ]    display this help screen
  [ -v | -vv ]       set verbose level to 1 or 2
  [ -n ]             normal conversion mode
  [ -d ]             dirty conversion mode


The '-d' or the '-n' option must be passed to set the conversion_mode.


set verbose level to 1 or 2 to get more info when running tasker_package_utils names command.
```

##### Examples:

```
#Convert tasker system privileged app to user app in normal mode
bash tasker_package_utils convert_user
```
##


- **`tasker_package_utils uninstall`**

**`tasker_package_utils uninstall`** command is used to to uninstall tasker. The tasker system privileged apk will also be removed provided that `tasker_package_utils convert_system_priv` command was used to install it as a system privileged app.

##### Usage:

```
tasker_package_utils uninstall command is used to uninstall tasker.
Usage:
  tasker_package_utils uninstall [command_options] tasker_config

Available command_options:
  [ -h | --help ]    display this help screen
  [ -v | -vv ]       set verbose level to 1 or 2
  

set verbose level to 1 or 2 to get more info when running tasker_package_utils uninstall command.
```

##### Examples:

```
#Uninstall tasker
bash tasker_package_utils uninstall
```
##


- **`tasker_package_utils perms`**

**`tasker_package_utils perms`** command is used to manage tasker package permissions. This command supports the script to be run directly on the device itself in a root shell like in termux or to be run over adb.

##### Usage:

```
tasker_package_utils perms command is used manage tasker package permissions.
Usage:
  tasker_package_utils perms [command_options] grant|revoke|list
  tasker_package_utils perms [command_options] grant|revoke permission_1 permission_2 ...

Available command_options:
  [ -h | --help ]    display this help screen
  [ -v | -vv ]       set verbose level to 1 or 2
  [ -a ]             run_mode adb
  [ -d ]             run_mode dev [default]
  [ -r ]             run_mode adb_root

The first argument passed sets the perms_mode of the perms command and must be equal to 'grant', \
'revoke' or 'list'.
- 'grant' mode grants permissions to the tasker package
- 'revoke' mode grants permissions to the tasker package
- 'list' mode lists all permissions granted to the tasker package

If no additional permission arguments are passed and perms_mode is 'grant' or 'revoke', then \
all uncommented permissions in the permissions_array at the start of this script are granted \
or revoked.

If any permission that is processed does not contain a dot '.', then 'android.permission.' is \
automatically prefixed to it.

The options '-a', '-d' and '-r' set the run_mode of the perms command.
- 'dev' if script is directly running on an android device like in termux
- 'adb' if script is running on a computer and you want to run commands over adb
- 'adb_root' if script is running on a computer and you want to run commands over adb with root

The 'adb_root' run_mode might be needed in case you are getting permission denied errors while using \
'adb' run_mode. The default run_mode is 'dev'.

set verbose level to 1 or 2 to get more info when running tasker_package_utils perms command.
```

##### Examples:

```
#Grant all uncommented permissions in the permissions_list array in tasker_package_utils script to tasker

#run in a root shell in your android device like in termux
bash tasker_package_utils perms grant

#or run over adb
bash tasker_package_utils perms -a grant

#Grant specific permission to tasker

#run in a root shell in your android device like in termux
bash tasker_package_utils perms grant "android.permission.READ_LOGS"

#or run over adb
bash tasker_package_utils perms -a grant "android.permission.READ_LOGS"

#if the permission passed does not contain a dot ".", then "android.permission." is automatically prefixed to it
bash tasker_package_utils perms grant "READ_LOGS"


#Revoke all uncommented permissions in the permissions_list array in tasker_package_utils script to tasker

#run in a root shell in your android device like in termux
bash tasker_package_utils perms revoke

#or run over adb
bash tasker_package_utils perms -a revoke


#Revoke specific permission from tasker

#run in a root shell in your android device like in termux
bash tasker_package_utils perms revoke "android.permission.READ_LOGS"

#or run over adb
bash tasker_package_utils perms -a revoke "android.permission.READ_LOGS"

#if the permission passed does not contain a dot ".", then "android.permission." is automatically prefixed to it
bash tasker_package_utils perms -a revoke "READ_LOGS"


#List all permissions granted to tasker. Wait a few seconds after permission is granted or revoked and tasker app is restarted for updates to take effect.

#run in a root shell in your android device like in termux
bash tasker_package_utils perms list

#or run over adb
bash tasker_package_utils perms -a list

#or run over adb with root if permission denied errors are received
bash tasker_package_utils perms -r list

#check if specific permission is granted to tasker
bash tasker_package_utils perms list | grep READ_LOGS
```
##


##### Dependencies:

You should have GNU sed installed in your system.
- Termux (non-root shell): `apt install sed`
- Linux distros: `sudo apt install sed`
- Windows: You can use cygwin installer.
##


##### Install Instructions For Termux In Android:

The `tasker_package_utils` file should be placed in termux `bin` directory `/data/data/com.termux/files/usr/bin` and it should have `termux` uid:gid ownership and have executable `700` permission before it can be run in the termux terminal without specifying its path.
1. Copy the file to termux bin directory:
	Either `cd` to the download/extraction directory and run following commands

	```
	cat tasker_package_utils > /data/data/com.termux/files/usr/bin/tasker_package_utils
	```

	Or use a file browser like root explorer to copy the file to the termux bin directory.

2. Set correct ownership and permission:
	Either run following commands to set them automatically, requires su binary to be in `$PATH`.

	```
	export termux_bin_path="/data/data/com.termux/files/usr/bin"; export owner="$(stat -c "%u" "$termux_bin_path")"; for f in tasker_package_utils; do if [ -f "$termux_bin_path/$f" ]; then su -c "chown $owner:$owner \"$termux_bin_path/$f\" && chmod 700 \"$termux_bin_path/$f\""; fi; done;
	```

	Or manually set them with your file browser. You can find `termux` `uid` and `gid` by running the command `id -u` in a non root shell in termux or by checking the properties of the termux `bin` directory from your file browser.

You may optionally run the script placed in the current directory without setting the ownership and permission by running the command `bash tasker_package_utils`.
##
