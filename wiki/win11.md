## Windows 11

* Disable Web results in Start Search:
  1. `regedit`
  2. `HKEY_CURRENT_USER\Software\Policies\Microsoft\Windows`
  3. New Key: `Explorer`
  4. New DWORD: `DisableSearchBoxSuggestions` Value: 1
