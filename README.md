<details>
  <summary><strong>📑 Table of Contents</strong></summary>

- [Why](#why)
- [Getting started](#getting-started)
- [Setting up the converter](#setting-up-the-converter)
  - [Method 1: Automatic Installation (recommended)](#method-1-automatic-installation-recommended)
  - [Method 2: Manual Installation (OPTIONAL)](#method-2-manual-installation-optional)
- [Running the tool](#running-the-tool)
  - [Converting console save to pc save](#converting-console-save-to-pc-save)
  - [Using spamton save editor](#using-spamton-save-editor)
  - [Converting pc save to console save](#converting-pc-save-to-console-save)
- [Final step](#final-step)
- [Credits](#credits)

</details>

# Why
Whether you're playing [atesquik's](https://discord.gg/ates-cellar-1158001681477402745) deltarune unofficial android port or emulating any console release of deltarune on your phone, you're dealing with `deltarune.sav` files (console saves). You can't directly use spamton save editor to edit these saves, as it only supports pc saves. This guide will tell you how to convert console saves to pc saves and vice versa entirely on an android device to enjoy deltarune with modified saves.

# Getting started
1. Copy your deltarune.sav file to somewhere you can directly access, i.e. copy your deltarune.sav from app's storage to your device's storage using supported file manager. This process varies depending on how you're playing the game (android port or console emulation). For atesquik's android port you can follow this [method](https://discord.com/channels/1158001681477402745/1327748080556183573/1392485803145302038). **For this guide, I'll be using atesquik's deltarune android port and I'll be putting my deltarune.sav file in Download folder of my device** (file path: `/storage/emulated/0/Download/deltarune.sav`).
> [!CAUTION]
> You should always keep multiple backups of your original save file, since editing and converting save files is always prone to damaging it or making unintended side effects in-game.
2. Get termux apk from [fdroid](https://f-droid.org/en/packages/com.termux/) or [github](https://github.com/termux/termux-app/releases) (universal apk or according to your device - 64/32 bit, also check android version of the apk) and install it.

# Setting up the converter
We'll be setting up the converter on our Android device now. This is a one-time process that you need to do only once after installing termux. **You can follow any of the following two ways of running commands.**
## Method 1: Automatic Installation (recommended)
Open termux and paste the following long command and press enter.
```bash
termux-setup-storage; cd; pkg up -y; pkg in git dotnet-sdk-8.0 -y; r=DeltaruneSaveConverter; git clone https://github.com/InvoxiPlayGames/$r; cd $r; dotnet build *.sln; d=~/DRSaveConverter; rm -rf $d; mkdir -p $d; cp -a bin/Debug/net8.0/* $d; cd; rm -rf $r; b=~/.bashrc; echo "export PATH=\$PATH:$d" >>$b; echo "alias drsave=$r" >>$b; . $b
```
Allow storage permission when prompted. Stay connected to data/wifi when running this.
> [!TIP]
> You can run this same command again to update the save converter tool.
## Method 2: Manual Installation (OPTIONAL)
Follow this only if you're sceptical about running the scary long command from the previous method, and you want to install it manually. **No need to do this if you have already ran the previous command.**
<details>
<summary><strong>Click to read (OPTIONAL)</strong></summary>
Here's a manual list of commands with short explanation of the steps to get, build and setup the tool step-by-step:

i. Allow Termux to access shared storage, please allow storage permission when prompted
`termux-setup-storage`

ii. Change to home directory
`cd`

iii. Update package lists and upgrade all packages, stay connected to data/wifi when running this
`pkg update -y`
`pkg upgrade -y`

iv. Install Git and .NET SDK 8.0, stay connected to data/wifi when running this
`pkg install git dotnet-sdk-8.0 -y`

v. Clone the Deltarune Save Converter repository from GitHub, stay connected to data/wifi when running this
`git clone https://github.com/InvoxiPlayGames/DeltaruneSaveConverter`

vi. Change into the cloned repository directory
`cd DeltaruneSaveConverter`

vii. Build the .NET solution in the repository
`dotnet build DeltaruneSaveConverter.sln`

viii. Create a directory to store the built converter tool
`mkdir -p ~/DRSaveConverter`

ix. Copy all built files to the new directory (ensuring it overwrites existing files for updating purposes, if any)
`cp -a --remove-destination bin/Debug/net8.0/* ~/DRSaveConverter`

x. Return to home directory
`cd`

xi. Remove the cloned GitHub repository to clean up
`rm -rf DeltaruneSaveConverter`

xii. Add the converter tool directory to PATH in .bashrc
`echo "export PATH=\$PATH:~/DRSaveConverter" >> ~/.bashrc`

xiii. Add a shortcut alias for running the tool
`echo "alias drsave='DeltaruneSaveConverter'" >> ~/.bashrc`

xiv. Reload the updated .bashrc
`source ~/.bashrc`
</details>

# Running the tool
This is a command line tool so you need to run the tool in termux by running commands.
## Converting console save to pc save
You can run just `drsave` or `DeltaruneSaveConverter` to get usage info of the tool. As the deltarune.sav file is in Download folder, run:
```bash
drsave ConvertFromConsole storage/downloads/deltarune.sav storage/downloads/deltarune_pcsaves
```
This converts the deltarune.sav file to pc save(s) and puts the pc saves at `deltarune_pcsaves` folder inside the Download folder.
> [!NOTE]
> You can also use other file paths such as `/storage/emulated/0/` (internal storage) or `/storage/0000-0000/` (SD card or other storage devices), but make sure that termux has read and write permission in these paths.
## Using spamton save editor
You can now upload the pc saves located at the `deltarune_pcsaves` folder to [Spamton save editor](https://saveeditor.spamton.com/) to edit them. For each chX files, (chapters 1, 2, 3, 4, ...) **filechX_0 is slot 1, filechX_1 is slot 2, filechX_2 is slot 3, and files 3-5 are only the "completion data"** which can be accessed at next chapter's saves menu when loading the next chapter from a previous chapter's complete save. After editing the save, download the edited save from the site and put them in `deltarune_pcsaves` folder.
## Converting pc save to console save
Since the edited pc save files are now in `deltarune_pcsaves` folder inside the Download folder, you can now run:
```bash
drsave ConvertFromPC storage/downloads/deltarune_pcsaves storage/downloads/deltarune_edited.sav
```
This converts the edited pc save(s) files to an edited console save file at `deltarune_edited.sav` inside the Download folder.
# Final step
Copy your `deltarune_edited.sav` file to the app's storage, delete your old deltarune.sav file from the app's storage, and rename the edited file to `deltarune.sav` so the game can recognise the file.
> [!WARNING]
> Make sure to keep a backup of original save before replacing it with the edited save! There is no turning back once you delete your original save.
# Credits
- Toby fox for creating UNDERTALE and deltarune
- Spamton save editor for making the save editor for pc save files of deltarune
- InvoxiPlayGames for making DeltaruneSaveConverter
- Termux dev team and all contributors for making termux
- atesquik for making the deltarune unofficial android port
