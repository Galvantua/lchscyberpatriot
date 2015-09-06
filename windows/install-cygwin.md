# install cygwin

## set bridged networking in vmware fusion

* In VMware Fusion (but not inside the VM)
	* type `Command-E`
	* choose **"Network Adapter"**
	* choose **"Bridged Networking"** - **"Autodetect"**
* Choose **"Work"** network when prompted in image

## open powershell (no need admin)

Start Menu...type `Powershell`...choose **"Windows PowerShell"** from the list

Copy the text below, right-click your PowerShell window, and hit `enter`

```
$client = new-object System.Net.WebClient
$client.DownloadFile( "http://cygwin.org/setup-x86.exe", "c:\Users\Public\setup-x86.exe" )
```

## open command prompt as administrator

Start Menu...type `Command Prompt`...right-click **"Command Prompt"** in list and choose **"Run as administrator"**

Copy the text below, right-click the **"Command Prompt"** window, and choose **"Paste"**

```
cd c:\Users\Public
edit runme.cmd
```

Copy the text below, right-click the **"Command Prompt"** window title bar, choose **"Edit...Paste"**

```
setup-x86.exe ^
--quiet-mode ^
--site http://mirrors.kernel.org/sourceware/cygwin/ ^
--root c:\cygwin ^
--packages ^
openssh,wget,perl,python,curl,rsync,git
```

* Type `Alt-F, s` to save
* Type `Alt-F, x` to exit

Run the `runme.cmd`

```
runme.cmd
```

## edit cygwin.bat file

```
edit c:\cygwin\cygwin.bat
```

* Move your cursor to the line immediately before the final bash line.
* Copy the text below, right-click the **"Command Prompt"** window title bar, choose **"Edit...Paste"**

```
set CYGWIN=binmode ntsec
```

* Type `Alt-F, s` to save
* Type `Alt-F, x` to exit

# [Win 7] set password for CyberPatriot user

* Passw0rd!

# [Win 7] start cygwin terminal as administrator

* Right-click **"Cygwin Terminal"** on Desktop and choose **"Run as administrator"**

# [Win 2008] start cygwin terminal as administrator

* Click **"Start Menu...All Programs...Cygwin"**
* Right-click **"Cygwin Terminal"** and choose **"Run as administrator"**

## [Win 7] configure sshd

```
$ ssh-host-config
```
> `*** Query: Should StrictModes be used? (yes/no)` **`yes`**

> `*** Query: Should privilege separation be used? (yes/no)` **`no`**

> `*** Query: Do you want to install sshd as a service?`

> `*** Query: (Say "no" if it is already installed as a service) (yes/no)` **`yes`**

> `*** Query: Enter the value of CYGWIN for the daemon: []` **`binmode ntsec`**

> `*** Query: Do you want to use a different name? (yes/no)` **`yes`**

> `*** Query: Enter the new user name:` **`CyberPatriot`**

> `*** Query: Reenter:` **`CyberPatriot`**

> `*** Query: Please enter the password for user 'CyberPatriot':` **`Passw0rd!`**

> `*** Query: Reenter:` **`Passw0rd!`**

## [Win 2008] configure sshd

```
$ ssh-host-config
```
> `*** Query: Should StrictModes be used? (yes/no)` **`yes`**

> `*** Query: Should privilege separation be used? (yes/no)` **`yes`**

> `*** Query: new local account 'sshd'? (yes/no)` **`yes`**

> `*** Query: Do you want to install sshd as a service?`

> `*** Query: (Say "no" if it is already installed as a service) (yes/no)` **`yes`**

> `*** Query: Enter the value of CYGWIN for the daemon: []` **`binmode ntsec`**

> `*** Query: Do you want to use a different name? (yes/no)` **`no`**

> `*** Query: Create new privileged user account 'WIN-2JFUJDRWO6B\cyg_server' (Cygwin name: 'cyg_server')? (yes/no)` **`yes`**

> `*** Query: Please enter the password:` **`Passw0rd!`**

> `*** Query: Reenter:` **`Passw0rd!`**

## start sshd server
```
cygrunsrv -S sshd
```

## open firewall
```
netsh advfirewall firewall add rule name="sshd" dir=in action=allow protocol=TCP localport=22
```

## test local ssh
```
ssh cyg_server@localhost
# enter 'Passw0rd!' when prompted
```	
