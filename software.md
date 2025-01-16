---
title: CBE 3300 Software
toc: true
colorlinks: true
---

\newpage

# Software you should install

- VS Code
- Python (Miniconda)
- Arduino IDE
- Git
- CAD of some form

Instructions for installing some of the programs are below. Refer to the official website for the latest installation instructions.

If using a different computer, or you just want to try a program out, you can often download a compressed archive (zip, tar, 7z, etc) -- usually from the official GitHub repository. Extract the files and run the executable to run the program without installing.  
*Note: this can also be used to avoid the need for admin rights.

## cbe3300 Python environment

Installation

1. Download `env-cbe3300.yaml`.
1. Run the following from an Anaconda Python distribution:
    
        conda env create --file env-cbe3300.yaml
1. Activate the environment with `conda activate cbe3300`.
    


# Mac

We'll use the terminal where we can. To open yours, use the spotlight search (`Cmd + Space`) or the keyboard shortcut (`Cmd + Shift + T`).

## VS Code

VS Code is part text editor, part IDE, part terminal, part content management system, part PDF viewer, part anything you can do in a browser. It's awesomely versatile and lightweight.

Download it here: [https://code.visualstudio.com/download](https://code.visualstudio.com/download).

## Git

Check if git is installed by typing `git`.

If not, check out the installation process here: [https://www.git-scm.com/download/mac](https://www.git-scm.com/download/mac). 

While git isn't required for this class, it's good practice to maintain your code in version control.

## Miniconda

Miniconda will be the environment manager we use for Python. It's lighter (fewer files to download) than Anaconda and provides the same functionality.

See the install page here: [https://docs.anaconda.com/free/miniconda/](https://docs.anaconda.com/free/miniconda/) or use the commands from that page:

```sh
mkdir -p ~/miniconda3
curl https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-arm64.sh -o ~/miniconda3/miniconda.sh
bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
rm -rf ~/miniconda3/miniconda.sh
```

Then:

```sh
~/miniconda3/bin/conda init bash
~/miniconda3/bin/conda init zsh
```

### Environment

Once installed, create an environment for CBE 3300. 

You can either do this manually or (recommended) download `env-cbe3300.yaml` and install from the spec. Make sure you're in the directory containing the file before running this command as written.

```sh
conda env create --file env-cbe3300.yaml
```

# Windows

## Miniconda

Install by downloading the executable or unpacking the zip file.

If using on a university computer, access it from the Anaconda/Miniconda prompt, rather than Command Prompt or PowerShell. Then open VS Code from within the *conda prompt.

### I can't open my terminal or command prompt anymore

https://answers.microsoft.com/en-us/windows/forum/all/fixed-cant-open-command-prompt-cmd-on-windows-10/4456f08d-bfd4-4484-be77-fb958ff202d8

Edit the AutoRun registry key. You can also delete it.