# Configure GIT

All Guides about Configuring GIT on git.zf.local


If you are using TortoiseGIT then follow [this tutorial](tortoise-git.md) to configure SSH key. You can still follow the following instruction and do the TortoiseGIT configurations additionally.

## How to Configure SSH Key

### Generate an SSH key pair

1. Use `ssh-keygen` to generate a key. Its wise to use <comment> as something memorable e.g. *zf.windows.key*

```bash
PS> ssh-keygen -t ed25519 -C "<comment>"
```

2. When asked press enter. You will see the following

```console
Generating public/private ed25519 key pair.
Enter file in which to save the key (/home/user/.ssh/id_ed25519):
```

3. Now copy this key to clip board

- **on windows use**

```bash
PS> cat ~/.ssh/id_ed25519.pub | clip
```

- **on linux use**

```bash
xclip -sel clip < ~/.ssh/id_ed25519.pub
```

### Add Keys to Gitlab

Now login to your git.zf.local account. On top right corner, clik on your avtar and then click on Preferences. After this, click on SSH Keys icon on left side menue. 

Now add your key in the text box. Gitlab will automatically add title (it will be your key comment from first step). By efault it will set an expiration date of 1 year. Now click on Add Key. Your key has been successfully added to ZF Gitlab account.

### SSH Setup on Windows
You need extra setup to configure SSH-Agent on windows. This is due to ssh-agent conflict delivered with git. This will pop annoying "Enter SSH Key asspharase" and will result in the failure of git clone commands.

Following commands need to be in Power Shell with admin priveliges.

#### Enabling and starting ssh-agent

Execute following command in Power Shell.

```bash
PS> Get-Service ssh-agent | Set-Service -StartupType Automatic0
```
If you get error like `Automatic0` not found then try `Automatic`. You can also use tab after `-StartupType` for autocompletion.

Now execute following command to check if the ssh paths are properly configured.

```bash
PS> Get-Command ssh | Select-Object Source
```
With this last command, you should get this output

```bash
Source
------
PS> C:\Windows\System32\OpenSSH\ssh.exe
```

In last step, now start ssh-agent by executing following command.

```bash
PS> ssh-agent

```

#### Importing SSH keys

Keys need to be imported to the ssh-agent service so that they can be unlocked for use. Execute the following and follow the prompts to load and unlock your keys.

```bash
PS> ssh-add
```

#### Linking to git.zf.local

Run the following command to update the environment variable:

```bash
PS> [Environment]::SetEnvironmentVariable("GIT_SSH", "$((Get-Command ssh).Source)", [System.EnvironmentVariableTarget]::User)
```
All settings are done. Now open anyother instance of Power Shell to active the new configurations.

### How to Handle Expired SSH Keys on Gitlab

If any of your SSH keys are expired then you can delete them from git.zf.local. You can use the existing key by re-importing them by following method.

1. Copy SSH key to clip board

- **on windows use**

```bash
PS> cat ~/.ssh/id_ed25519.pub | clip
```

- **on linux use**

```bash
xclip -sel clip < ~/.ssh/id_ed25519.pub
```

2. Import the Keys to Gitlab

Now login to your git.zf.local account. On top right corner, clik on your avtar and then click on Preferences. After this, click on SSH Keys icon on left side menue. 

Now add your key in the text box. Gitlab will automatically add title (it will be your key comment from first step). By default it will set an expiration date of 1 year. Now click on Add Key. Your key has been successfully added to ZF Gitlab account.


## Ignore GIT SSL Verify

```
