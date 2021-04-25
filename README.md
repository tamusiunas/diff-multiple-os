# diff-multiple-os

Bash scripts to allow the use of GNU patch and diff commands in multiple environments, Linux, MacOS and Windows. The path is automatically changed depending on the platform.

Windows Requirements:

- [Git-SCM](https://git-scm.org) - It provides and add a bash.exe to PATH

or 

- [WSL](https://docs.microsoft.com/en-us/windows/wsl/install-win10) - It provides a Linux on Windows


### patch.bash
```bash
Usage: 
           $ bash ./patch.bash "<patch parameters>"
Important: "<patch parameters>" MUST have double quotes.
           Without double quotes Windows can't interprept Windows-style PATH
Usage example: 
           $ bash ./patch.bash "c:\devel\prog1\file.cpp 'c:\Users\User 1\file.cpp.diff'"
For more information about patch parametes: 
           $ man patch # or <https://man7.org/linux/man-pages/man1/patch.1.html>
```

### diff.bash
```bash
Usage: 
           $ bash ./diff.bash "<diff parameters>"
Important: "<diff parameters>" MUST have double quotes.
           Without double quotes Windows can't interprept Windows-style PATH
Usage example: 
           $ bash ./diff.bash "'c:\Users\User 1\file.cpp.diff' c:\devel\prog1\file.cpp"
For more information about diff parametes: 
           $ man diff # or <https://man7.org/linux/man-pages/man1/diff.1.html>
```

## Usage example on [PlatformIO](https://platformio.org) Project
### platformio.ini
```
[env:esp32doit-devkit-v1]
platform = espressif32     
board = esp32dev
upload_speed=115200 
framework = arduino
...
extra_scripts = pre:apply_patch.py

```

### apply_patch.py
```python
Import ("env")
...
env.Execute("bash -c \"patches/patch.bash '%s %s'\"" % (originalFile, patchFile)) # patch.bash must be into patches directory
```
