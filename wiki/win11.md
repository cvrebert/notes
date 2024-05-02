## Windows 11

* Disable Web results in Start Search:
  1. `regedit`
  2. `HKEY_CURRENT_USER\Software\Policies\Microsoft\Windows`
  3. New Key: `Explorer`
  4. New DWORD: `DisableSearchBoxSuggestions` Value: 1
* Disable security questions as an option for resetting local account passwords:
  1. `regedit`
  2. `HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\System`
  3. New DWORD: `NoLocalPasswordResetQuestions` Value: 1
  4. (Allegedly) Change your password
