# **Setup for the tutorial**

## **1) Install the Compiler**

### **a) Windows (_eww_)**

1.  Install **Chocolatey** by entering the following in _Command Prompt_ (**not PowerShell**):

    ```batch
    @"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "[System.Net.ServicePointManager]::SecurityProtocol = 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
    ```

2.  Then install `gcc` using **choco** :

    ```batch
    $ choco install mingw -y

    $ choco upgrade mingw
    ```

### **b) Linux (_the Gods_)**

Perform the following one-time setup :

```bash

$ sudo apt install build-essential

$ sudo apt install manpages-dev

```

### **c) Mac (_lucky you_)**

Install **clang** using [**homebrew**](https://brew.sh/). It is a widely used package-manager on Mac.

```zsh
$ # Install Brew :
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

> Make sure _HomeBrew_'s **bin** is on **PATH**.

```zsh
$ # Install Clang :
$ brew install llvm
$ brew upgrade llvm
```

---

## **2) INSTALLING VSCODE**

### **a) Windows**

1.  Visit [VSCode](https://code.visualstudio.com).
2.  Download the Windows-64 'Stable' version.
3.  Follow the installation steps by running the downloaded file, and check the **ADD VSCode to PATH** option for sure.

### **b) Linux**

- Install using [**snap**](https://snapcraft.io/code). Choose your distro type in the list to install **snap**.

- **snap** is a new global package-manager common to all distros.

```bash
# For example, on Debain-based systems :

# To install snap :
$ sudo apt update
$ sudo apt install snapd

# To install VSCode :
$ sudo snap install code --classic
```

### **c) Mac**

1.  Visit [VSCode](https://www.code.visualstudio.com).
2.  Download the MacOS 'Stable' version.
3.  Follow the installation steps by running the downloaded file

(OR)

Install it using **HomeBrew**

```bash
$ # Install VSCode :
$ brew update
$ brew tap caskroom/cask
$ brew cask search visual-studio-code
$ brew cask install visual-studio-code
```

---

## **3) Setup VSCode**

### **a) Install the Extensions**

- Search for the C/C++, and C++ Intellisense extensions and install them.
- You get language-support, auto-complete and intellisense features through these extensions.

> ### Create a **.vscode** folder in your project root.

### **b) `tasks.json` file**

1. Create a **`tasks.json`** file in **.vscode**
1. Add the following to the file :

```json
{
	"version": "2.0.0",
	"type": "shell",

	// General console config
	"presentation": {
		"focus": true,
		"panel": "shared",
		"showReuseMessage": false,
		"clear": true,
		"echo": false
	},
	"tasks": [
		// Compile Task
		{
			"type": "shell",
			"label": "Compile",
			"command": "/usr/bin/gcc",
			"args": [
				"-g",
				"-O2",
				"${file}",
				"-o",
				"out/${fileBasenameNoExtension}.out"
			],
			"options": {
				"cwd": "${workspaceFolder}"
			},
			"group": "build",
			"windows": {
				"command": "gcc",
				"args": [
					"-g",
					"-O2",
					"${file}",
					"-o",
					"out/${fileBasenameNoExtension}.exe"
				],
				"problemMatcher": "$msCompile"
			},
			"osx": {
				"command": "clang",
				"args": [
					"-g",
					"-O2",
					"${file}",
					"-o",
					"out/${fileBasenameNoExtension}.out"
				]
			}
		},

		// Run Task
		{
			"type": "shell",
			"label": "Run",
			"command": "out/${fileBasenameNoExtension}.out",
			"promptOnClose": false,
			"dependsOn": ["Compile"],
			"group": {
				"kind": "build",
				"isDefault": true
			},
			"windows": {
				"command": "out/${fileBasenameNoExtension}.exe"
			}
		}
	]
}
```

### **c) `c_cpp_properties.json` file**

1. Create a **c_cpp_properties.json** file in **.vscode**
2. Add the following to the file.

```json
{
	"configurations": [
		{
			"name": "Windows",
			"includePath": ["${workspaceFolder}/**"],
			"defines": ["_DEBUG", "UNICODE", "_UNICODE"],
			"compilerPath": "C:/ProgramData/chocolatey/lib/mingw/tools/install/mingw64/bin/gcc.exe",
			"cStandard": "c18",
			"intelliSenseMode": "gcc-x64"
		},
		{
			"name": "Linux",
			"includePath": ["${workspaceFolder}/**"],
			"defines": ["_DEBUG", "UNICODE", "_UNICODE"],
			"compilerPath": "/usr/bin/gcc",
			"cStandard": "c18",
			"intelliSenseMode": "gcc-x64"
		},
		{
			"name": "Mac",
			"includePath": ["${workspaceFolder}/**"],
			"defines": ["_DEBUG", "UNICODE", "_UNICODE"],
			"cStandard": "c18",
			"intelliSenseMode": "clang-x64"
		}
	],
	"version": 4
}
```

> Happy Coding!
