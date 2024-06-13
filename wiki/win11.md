## Windows 11

* Disable Web results in Start Search:
  1. `regedit`
  2. `HKEY_CURRENT_USER\Software\Policies\Microsoft\Windows`
  3. New Key: `Explorer`
  4. New DWORD: `DisableSearchBoxSuggestions` Data value: 1
* Disable security questions as an option for resetting local account passwords:
  1. `regedit`
  2. `HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\System`
  3. New DWORD: `NoLocalPasswordResetQuestions` Data value: 1
  4. (Allegedly) Change your password
* Permanently disable "Sign in to your Microsoft account" [nag](https://www.deceptive.design/types/nagging) notification in the Start Menu, that only offers a "Remind me later" option and no "Never ask again" option.
  1. `regedit`
  2. `HKEY_CURRENT_USER\Software\Policies\Microsoft\Windows\CurrentVersion\AccountNotifications`
  3. New DWORD: `DisableAccountNotifications` Data value: 1
* [ElevenForum: Disable ads in Windows 11](https://www.elevenforum.com/t/disable-ads-in-windows-11.8004/)
* Disable tracking that's not even utilized anymore:
  * Settings ❯ Privacy & security ❯ Activity history
