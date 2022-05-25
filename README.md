# VSConan - Conan Extension for Visual Studio Code

[![Marketplace VSConan](https://img.shields.io/visual-studio-marketplace/v/afri-bit.vsconan)](https://marketplace.visualstudio.com/items?itemName=afri-bit.vsconan)
![Rating](https://img.shields.io/visual-studio-marketplace/r/afri-bit.vsconan)
![Downloads](https://img.shields.io/visual-studio-marketplace/d/afri-bit.vsconan)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
[![Donate](https://img.shields.io/badge/Donate-PayPal-blue.svg)](https://www.paypal.com/paypalme/afribit)

<p align="center">
<img src="https://raw.githubusercontent.com/afri-bit/vsconan/main/resources/icon/vsconan-logo.png" width="50%">
</p>

## Introduction 

The **VSConan** extension helps you manage the conan local cache on your machine. It gives you easy access to your local cache and allows you to manage it by using integrated explorer in the Visual Studio Code without typing a single line of command in the terminal. **VSConan** provides variety of features, including a quick overview of installed packages, renaming and duplicating profiles, enabling and disabling remotes and more. For more information see [Extension Features](#extension-features).

![Recording of VSConan Explorer](https://raw.githubusercontent.com/afri-bit/vsconan/main/resources/img/demo_explorer.gif)

## Prerequisites
1. [Python](https://www.python.org/) with [conan](https://pypi.org/project/conan/) installed using `pip`
2. Conan installed on your system using [alternative installations](https://conan.io/downloads.html)

## How To Start

**VSConan** contributes to official VS Code configurations (`settings.json`), where you can configure the environment to use this extension. To start you can configure following settings  in the `settings.json`:
  * `vsconan.general.pythonInterpreter": "python"`  
    Path to the python interpreter executable. It doesn't have to be a path but can be also an alias as you can see in the default value above, in case you already defined python in your environment variables.  
    Default value: `python`
  * `vsconan.general.conanExecutable": "conan"`  
    Path to the conan executable, in case you install conan using [alternative installations](https://conan.io/downloads.html).  
    Defautl value: `conan`
  * `vsconan.general.conanExecutionMode": "conanExecutable"`  
    Setting to switch the mode how the extension executes conan command, either using python oder directly conan executable. We leave the conanExecutable as default, because even if you install conan using `pip`, python will create an 'executable' called `conan`, that can be executed globally.  
    Based on the option selected, the chosen path will be used to interact with conan.  
    Default value: `conanExecutable`  
    Possible options: [`conanExecutable`, `pythonInterpreter`]

If your system is set according to the default values of the settings, then you can start using the extension without tweaking the configurations.

If your prefer GUI solution to tweak this configuration, go to `File` > `Preferences` > `Settings` > `Extensions` > `VSConan`, and you will get the following view

![VSConan GUI Settings](resources/img/vsconan_gui_settings.png)


## Extension Features
The **VSConan** extension contains two major groups of features, one of them is the [Conan Explorer](#conan-explorer), where you can use to manage your local cache, and the other one is [Conan Workspace](#conan-workspace), where you can save your configuration of different conan flow commands in your VSCode workspace.

### Conan Explorer

![Recording of VSConan Explorer](https://raw.githubusercontent.com/afri-bit/vsconan/main/resources/img/demo_explorer.gif)

The **VSConan** extension contributes a Conan Explorer view to VS Code. The Conan Explorer lets you examine and manage important assets of your conan local cache, such as recipe, binary packages, profile and remote.

#### Conan Recipe

In the Conan Recipe explorer you can have an overview of the installed conan recipe in your local cache. 

![](https://raw.githubusercontent.com/afri-bit/vsconan/main/resources/img/conan_recipe_treeview.png)

As you can see in the picture above, there are several inline options on each item in the treeview.
* _Information_  
  Open a web view in VS Code editor, that contains information about this selected recipe. Currently the web view only shows a plain JSON text, that is obtained from the Conan CLI. 
* _Open in Explorer_  
  Open the the recipe path in the explorer
* _Open in VS Code_  
  Open the selected recipe in a new VS Code window
* _Remove_  
  Remove the selected recipe
#### Conan Binary Package

By selecting the recipe, the corresponded binary packages will be shown in this treeview.

![](https://raw.githubusercontent.com/afri-bit/vsconan/main/resources/img/conan_package_treeview.png)

Each item of this treeview has following options to offer:
* _Open in Explorer_  
  Open the selected binary package in the explorer
* _Open in VS Code_  
  Open the selected binary package in a new VS Code window
* _Remove_  
  Remove the selected binary package

#### Conan Profile

All the profiles that you saved on your machine will be listed in this explorer. By pressing `+` button on top right corner of the treeview, you can create a new empty profile.

![](https://raw.githubusercontent.com/afri-bit/vsconan/main/resources/img/conan_profile_treeview.png)

As the other treeviews, each item of this treeview contains several functionalities:
* _Edit_  
  Open the selected profile in the VS Code editor
* _Open in Explorer_  
  Open the selected profile in the file explorer
* _Rename_  
  Rename the selected profile
* _Duplicate_  
  If you want to change a small detail from a certain profile but you do not want to lose the original profile, we provide you this duplicate option to fulfill your purpose.
* _Remove_  
  Remove the selected profile

#### Conan Remote

Finally we come to the last part of this explorer, which is the explorer of the conan remote.  
The explorer itself provides you following options:
* _Edit_  
  Since the collection of remotes in conan is defined in one file called `remotes.json`, this option is not available of each remote item in the treeview. This will open `remotes.json` file in the VS Code editor instead.
* _Add_  
  Add a new remote

![](https://raw.githubusercontent.com/afri-bit/vsconan/main/resources/img/conan_remote_treeview.png)

As other treeview, each item is equipped with several options, that you can use to maintain your remotes.
* _Rename Remote_  
  Rename the selected remote
* _Update URL_  
  Modify the URL in the selected remote
* _Enable Remote_  
  Enable the selected remote. Enabled remotes can be seen from the icon next to the remote name. The remote `conancenter` in the picture above is enabled. 
* _Disable Remote_  
  Disable the selected remote. Disabled remotes can be seen from the icon next to the remote name. The remote `anyOtherRemote` in the picture above is disabled. 
* _Remove Remote_  
  Remove the selected remote

### Conan Workspace

The Conan Workspace feature provides you configuration file, that can be used to execute predefined conan flow command and its arguments. The configuration will be stored under `.vsconan` folder in your workspace.  
If you work a lot with conan and use VS Code as your IDE, this feature can be really beneficial for you. It can spare you some seconds by avoiding to type same command, maybe with different arguments in your terminal over and over again. Instead you can save the command that you want to execute in the configuration and reuse in the next execution. In addition to that, the configuration file is reusable, and can be distributed to other people, if you work in a team.

![Recording of VSConan Workspace](https://raw.githubusercontent.com/afri-bit/vsconan/main/resources/img/demo_workspace.gif)

**VSConan** Extension will detect your workspace as conan workspace, if it contains a `conanfile.py` or `conanfile.txt`, and will a show dialog box as following

![](https://raw.githubusercontent.com/afri-bit/vsconan/main/resources/img/prompt_conan_project.png)

If you choose yes, **VSConan** will generate a default configuration file in your workspace to start with.  
If you want to configure your workspace manually, we also provide you possibility to create a default configuration file using VS Code command `VSConan: Create Workspace Configuration (JSON)`.

Currently supported conan command for configuration file:
* create
* install
* build
* source
* package
* export-pkg

The default configuration file can be seen as following. You can extend the list of each command to have different name, description, user, channel and many other details. 

```json
{
    "python": "python",
    "commandContainer": {
        "create": [
            {
                "name": "create",
                "description": "Create command",
                "detail": "Create command detail",
                "conanRecipe": "conanfile.py",
                "profile": "default",
                "user": "",
                "channel": "",
                "args": []
            }
        ],
        "install": [
            {
                "name": "install",
                "description": "Install command",
                "detail": "Install command detail",
                "conanRecipe": "conanfile.py",
                "installFolder": "install",
                "profile": "default",
                "user": "",
                "channel": "",
                "args": []
            }
        ],
        "build": [
            {
                "name": "build",
                "description": "Build command",
                "detail": "Build command detail",
                "conanRecipe": "conanfile.py",
                "installFolder": "install",
                "buildFolder": "build",
                "packageFolder": "package",
                "sourceFolder": "source",
                "args": []
            }
        ],
        "source": [
            {
                "name": "source",
                "description": "Source command",
                "detail": "Source command detail",
                "conanRecipe": "conanfile.py",
                "installFolder": "install",
                "sourceFolder": "source"
            }
        ],
        "pkg": [
            {
                "name": "pkg",
                "description": "Package command",
                "detail": "Package command detail",
                "conanRecipe": "conanfile.py",
                "installFolder": "install",
                "buildFolder": "build",
                "packageFolder": "package",
                "sourceFolder": "source"
            }
        ],
        "pkgExport": [
            {
                "name": "pkg_export",
                "description": "Package export command",
                "detail": "Package export command detail",
                "conanRecipe": "conanfile.py",
                "installFolder": "install",
                "buildFolder": "build",
                "packageFolder": "package",
                "sourceFolder": "source",
                "args": []
            }
        ]
    }
}
```

### Additional Support Features

* `VSConan: Create Workspace Configuration (JSON)`  
  Create workspace configuration file
* `VSConan: Open Workspace Configuration (JSON)`  
  Open the workspace configuration file in the editor

## Release Notes
Detailed release notes are available [here](CHANGELOG.md).

## Contributing

See [the contribution guidelines](CONTRIBUTING.md) for ideas and guidance on how to improve the extension.

## Code of Conduct
See [Code of Conduct](CODE_OF_CONDUCT.md).

## Donation
If this extension is useful and can save some of your time during your productive day, I would really appreciate [a cup of coffee](https://www.paypal.com/paypalme/afribit) to keep me awake to continue developing this extension.

## Credits
Demonstration video for GIF was recorded using [Chronicler](https://marketplace.visualstudio.com/items?itemName=arcsine.chronicler).

## License

[MIT](LICENSE)
