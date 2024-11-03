---
title: Module 1
aliases:
  - "AZ-104 Module 1: Prerequisites for Azure administrators"
draft: false
tags:
  - "#AZ-104"
  - Microsoft
  - Cloud
author:
  - Sarthak Chandajkar
---
#  Prerequisites for Azure administrators

## Azure Cloud Shell
- browser accessible CLI experience
- Manage AZ resources
- Flexible to choose
	- Bash
	- Powershell
- authenticated/interactive
- not part of local machine
- provides cloud storage to keep files like SSH keys, scripts
- access important files between sessions and with different machines
- **Cloud Shell Editor**: make changes to files like scripts; saved directly to cloud storage from CSI.

## How does Azure Cloud Shell Work?

1. Access Cloud Shell
	1. From direct link
	2. From Azure Portal
	3. From code snippets (Microsoft Learn)

		![[Pasted image 20241029124859.png]]
	4. Select Shell Experience - PowerShell/Bash
	5. Start managing Resources.
- Upon opening a Cloud Shell session, a temporary host is allocated to the session with a preconfigured VM.
- Cloud Shell terminates after 20 mins of inactivity.
- Files are persistent on CloudDrive.

2. Access your own scripts and files.
	1. [[Azure CloudDrive]]
	2. access files on multiple devices
	3. Cloud Shell also lets you map an Azure Storage File Share, which is tied to a specific region.
### Cloud Shell Add-ons

| Category           | Name                                                                                                                                                                       |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Linux tools**    | bash  <br>zsh  <br>sh  <br>tmux  <br>dig                                                                                                                                   |
| **Azure tools**    | Azure CLI and [Azure classic CLI](https://github.com/Azure/azure-xplat-cli)  <br>AzCopy  <br>Azure Functions CLI  <br>Service Fabric CLI  <br>Batch Shipyard  <br>blobxfer |
| **Text editors**   | code (Cloud Shell editor)  <br>vim  <br>nano  <br>emacs                                                                                                                    |
| **Source control** | git                                                                                                                                                                        |
| **Build tools**    | make  <br>maven  <br>npm  <br>pip                                                                                                                                          |
| **Containers**     | Docker Machine  <br>Kubectl  <br>Helm  <br>DC/OS CLI                                                                                                                       |
| **Databases**      | MySQL client  <br>PostgreSql client  <br>sqlcmd Utility  <br>mssql-scripter                                                                                                |
| **Other**          | iPython Client  <br>Cloud Foundry CLI  <br>Terraform  <br>Ansible  <br>Chef InSpec  <br>Puppet Bolt  <br>HashiCorp Packer  <br>Office 365 CLI                              |

##  When should you use Azure Cloud Shell?

- when you are not using your default administrative device
- Open a secure command-line session from any browser-based device.
- Interact with Azure resources without the need to install plug-ins or add-ons to your device.
- Persist files between sessions for later use.
- Use either Bash or PowerShell, whichever you prefer, to manage Azure resources.
- Edit files (such as scripts) via the Cloud Shell editor.

##  When shouldn't you use Azure Cloud Shell?

- You intend to leave a session open for more than 20 minutes for long running scripts or activities. In these cases, your session is disconnected without warning, and the current state is lost.
- You need admin permissions, such as sudo access, from within the Azure CLI or PowerShell environment.
- You need to install tools that aren't supported in the limited Cloud Shell environment, but instead require an environment such as a custom virtual machine or container.
- You need storage from different regions. You might need to back up and synchronize this content since only one region can have the storage allocated to Azure Cloud Shell.
- You need to open multiple sessions at the same time. Azure Cloud Shell allows only one instance at time and isn't suitable for concurrent work across multiple subscriptions or tenants.
---

# Introduction to Bash

- Bash: standard shell scripting language for [[Linux]]
- *"**B**ourne **A**gain **Sh**ell"*
- **Shell**: program that commands the operating system to perform actions
- Bash became the de facto Linux standard. That's because Bash is compatible with Unix's first serious shell, the Bourne shell, also known as sh.
- built-in commands
- ability to invoke external programs.
- based on [[Unix Design Philosophy]]
- In Unix/Linux, everything is a file.
- you can use the same commands without worrying about whether the I/O stream—the input and output—comes from a keyboard, a disk file, a socket, a pipe, or another I/O abstraction.

## Bash Fundamentals

Bash Command Syntax: 

```bash
command [options] [arguments]
```

- ls - command to display the contents of the current working directory/another directory.
- Flags : Most Bash commands have options for modifying how they work. Options, also called _flags_, give a command more specific instructions.
- `man`:  To learn about the options for a command, use the `man` (for "manual")
- `--help`: This shows a description of the command's syntax and options.

## Use Wildcards
- Wildcards are symbols that represent one or more characters in Bash commands.
- Eg: *

> [!NOTE] Linux
> Linux has no formal concept of a file-name extension as other operating systems do. This doesn't mean that PNG files won't have a **.png** extension. It simply means Linux attaches no special significance to the fact that the file names end with **.png**.

- `cat`: check contents of file
- `sudo`: commands can only be run by the root user; a system administrator or superuser.
- [[at.deny]]
- `cd`: change directory
- `mkdir`: create new directory
- `rmdir`: removes directory if empty
- `rm`: remove/delete files
- `rm -i`: gives you option to think before deleting.
- `rm -rf /`: deletes every file on n entire drive.It works by recursively deleting all the subdirectories of root and their subdirectories. The `-f` (for "force") flag compounds the problem by suppressing prompts. _Don't do this._
- `cp`: copies not just files, but entire directories (and subdirectories)
- `-i`: interactive
- `ps`: gives you a snapshot of all the currently running processes. By itself, with no arguments, it shows all your shell processes; in other words, not much.
- [[ps-ef]]
- [[ps aux vs ps-ef]]
- `w`:  *"who";* find out who is on the servers.shows user names, their IP addresses, when they logged in, what processes they're currently running, and how much time those processes are consuming. It's a valuable tool for sysadmins.
- `sort`: sort text in alphabetical order
- `grep`: a command-line utility for searching plaintext datasets for lines that match a regular expression.
- `fmt`: format files
- `pr`: pagination
- `lpr`: sends the paginated output to the printer.
- `pwd`: "print working directory"; It prints the long-form path to what directory you're in now.
- `.`: current directory
- `..`: parent directory
- `.bash_history` is a special Bash file where all commands that you enter into the shell are stored. Bash remembers your command history, which, as we see later, is useful.
- `.bash_logout` is another special Bash file that is read and run every time a sign-in shell exists. Linux superusers can modify it to customize your environment.
- `.bashrc` is an important Bash configuration file that runs whenever you start a new shell. If you decide to open this file to look at it, be careful about making changes, because they can have unintended consequences.
- `~`: home directory
- `:wq`: write quit
- `&`: runs a command in the background and brings the user back to the command line.
- `kill`: kills a running process based on its process ID.
- `killall`: kills a process based on the process name.

## Bash I/O Operators

- `<` for redirecting input to a source other than the keyboard
- `>` for redirecting output to destination other than the screen
- `>>` for doing the same, but appending rather than overwriting
- `|` for piping output from one command to the input of another
---

# Introduction to PowerShell

- cli and scripting language all in one.
- designed as a task engine that uses cmdlets to wrap tasks that people need to do.
- framework to automate administrative tasks in Windows

## Features 
- **Built-in help system**
- Pipeline:
	- Powershell operates on <span style="background:#ff4d4f">objects over texts</span>.
- Aliases
- **It has cmdlets**: Commands in PowerShell are called cmdlets (pronounced _commandlets_). In PowerShell, cmdlets are built on a common runtime rather than separate executables as they are in many other shell environments. This characteristic provides a consistent experience in parameter parsing and pipeline behavior. Cmdlets typically take object input and return objects. The core cmdlets in PowerShell are built in .NET Core, and are open source.
- **It has many types of commands**
	- native exectutables
	- cmdlets
	- functions
	- scripts
	- aliases

To verify PowerShell Version use:

```
$PSVersionTable
```

For a more detailed version: 

```
$PSVersionTable.PSVersion
```

## Cmdlets

- compiled command
- developed in .NET or .NET Core 
- invoked as a command within PowerShell
- named according to a verb-noun naming standard

Three core cmdlets allow you to delve into what cmdlets exist and what they do:

- **Get-Command**: The `Get-Command` cmdlet lists all of the available cmdlets on your system. Filter the list to quickly find the command you need.
- **Get-Help**: Run the `Get-Help` core cmdlet to invoke a built-in help system. You can also run an alias `help` command to invoke `Get-Help` but improve the reading experience by paginating the response.
- **Get-Member**: When you call a command, the response is an object that contains many properties. Run the `Get-Member` core cmdlet to drill down into that response and learn more about it.
