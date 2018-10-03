---
title: Issue with debugging and installing C# dependencies - VS Code
date: 2017-09-11 16:30:12
tags:
---

**Issue with downloading Visual Studio Code debugger or omnisharp required for debugging C# in VS code - mostly behind corporate firewall**  

**Error details:**

```
Installing C# dependencies...
Platform: win32, x86_64

Downloading package '.NET Core Debugger (Windows / x64)'     Retrying from 'https://vsdebugger.blob.core.windows.net/coreclr-debug-1-14-7/coreclr-debug-win7-x64.zip' 
Installing package '.NET Core Debugger (Windows / x64)'
Failed at stage: installPackages
Error: end of central directory record signature not found

Finished
```


Installing C# dependencies...
Platform: win32, x86_64

---

**Fix:** 

In order to fix this issue, follow the instructions given below:  

- Download packages from the URL mentioned in the above error and place them in location:  
C:\Users\UserName\.vscode\extensions\ms-vscode.csharp-1.14.0\.debugger
  and for omnisharp copy the files in:  
C:\Users\UserName\.vscode\extensions\ms-vscode.csharp-1.14.0\.omnisharp

This should fix the issue.

Happy coding!