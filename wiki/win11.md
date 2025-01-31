## Windows 11

* Permanently disable "Sign in to your Microsoft account" [nag](https://www.deceptive.design/types/nagging) notification in the Start Menu, that only offers a "Remind me later" option and no "Never ask again" option.
  1. Settings ❯ Personalization ❯ Start ❯ Show account related notifications occasionally in Start
  2. Done. Registry-based alternative: `regedit`
  3. `HKEY_CURRENT_USER\Software\Policies\Microsoft\Windows\CurrentVersion\AccountNotifications`
  4. New DWORD: `DisableAccountNotifications` Data value: 1
* [ElevenForum: Disable ads in Windows 11](https://www.elevenforum.com/t/disable-ads-in-windows-11.8004/)
* Disable tracking that's not even utilized anymore:
  * Settings ❯ Privacy & security ❯ Activity history
* Edge:
  1. Navigate to `edge://flags`
  2. Search for and disable anything involving "Bing".

### Development
* [WSL file paths](https://learn.microsoft.com/en-us/windows/wsl/setup/environment#file-storage)
