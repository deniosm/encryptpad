Screenshots and tutorials are at [evpo.net/encryptpad/](http://evpo.net/encryptpad/)

# EncryptPad

![README.png](README.png)

<div id="cutline"></div>
EncryptPad is an application for viewing and editing symmetrically encrypted text. Using a simple and convenient graphical and command line interface, EncryptPad provides a tool for encrypting and decrypting binary files on disk while offering effective measures for protecting information, and it uses the most widely chosen quality file format **OpenPGP** [RFC 4880](https://tools.ietf.org/html/rfc4880). Unlike other OpenPGP software which main purpose is asymmetric encryption, the primary focus of EncryptPad is symmetric encryption.

## Table of Contents

* [Features](#features)
* [Supported platforms](#supported-platforms)
* [Why use EncryptPad?](#why-use-encryptpad)
* [When do I need EncryptPad?](#when-encryptpad)
* [When can I not use EncryptPad?](#when-can-i-not)
* [File types](#file-types)
  - [GPG](#gpg)
  - [EPD](#epd)
  - [Feature support](#feature-support)
* [What is an EncryptPad key file?](#key-file)
* [EPD file format when encrypting with a key](#epd-file-format)
* [Use CURL to automatically download keys from a remote storage](#use-curl)
* [Known weaknesses](#known-weaknesses)
* [Command line interface](#command-line-interface)
  - [encryptcli](#command-line-encryptcli)
  - [encryptpad](#command-line-encryptpad)
* [Installing EncryptPad](#installing)
    - [Portable executable](#portable-exe)
    - [Arch Linux](#install-on-arch)
    - [Ubuntu or Linux Mint](#install-on-ubuntu)
* [Compile EncryptPad on Windows](#compile-on-windows)
  - [Prerequisites](#prerequisites)
  - [Steps](#steps)
* [Compile EncryptPad on macOS](#compile-on-macos)
* [Compile EncryptPad on Linux](#compile-on-linux)
    - [Fedora](#build-on-fedora)
    - [Ubuntu](#build-on-ubuntu)
    - [Debian](#build-on-debian)
    - [openSUSE](#build-on-opensuse)
    - [Archlinux](#build-on-archlinux)
    - [FreeBSD](#build-on-freebsd)
	- [VoidLinux](#build-on-voidlinux)
* [Portable mode](#portable-mode)
* [FakeVim mode](#fakevim-mode)
    - [FakeVim: input and output commands](#fakevim-input-output)
* [Does EncryptPad store passphrases in the memory to reopen files?](#passphrases-in-memory)
* [Acknowledgements](#acknowledgements)
* [EncryptPad integrity verification](#integrity-verification)
    - [OpenPGP signing and certification authority](#openpgp-signing)
    - [Step by step verification process](#verification-process)
* [License](#license)
* [Contact and feedback](#contact)


<div id="features"></div>

## Features

* **Symmetric** encryption
* **Passphrase** protection
* **Key file** protection
* Combination of **passphrase and key file**
* Random **key file generator** 
* **Key repository** in a hidden directory in the user's home folder
* Path to a key file can be stored in an encrypted file. If enabled, **you do not need to specify the key file** every time you open files.
* Encryption of **binary files** (images, videos, archives etc.)
* **FakeVim** mode to edit files by using Vim-like user interface
* **Read only** mode to prevent accidental file modification
* **UTF8** text encoding
* Windows/Unix **configurable line endings**
* Customisable **passphrase generator** helps create strong random passphrases.
* File format compatible with **OpenPGP**
* **Iterated and salted S2K**
* **Passphrases are not kept in the memory** for reuse, only S2K results ([more ...](#passphrases-in-memory))
* Cipher algorithms: **TripleDES, CAST5, AES, AES192, AES256, Camellia128, Camellia192, Camellia256, Twofish**
* Hash algorithms: **SHA-1, SHA-256, SHA-384, SHA-512, SHA-224**
* Integrity protection: **SHA-1**
* Compression: **ZLIB, ZIP, Bzip2**
* **ASCII armor**
* **Large multi-gigabyte files** are supported

<div id="supported-platforms"></div>

## Supported platforms

* Windows

* Linux

* Mac OS

<div id="why-use-encryptpad"></div>

## Why use EncryptPad?

* **Multi-platform** codebase: it has been compiled on three popular operating systems and can be adapted to more.

* **Portable**: simply copy the executable to a memory stick or a network drive and use on all your computers.

* **Simple to use**: EncryptPad is a text editor and an encryption tool for binary files but it saves encrypted, compressed and integrity protected files.

* **Open source** with concise codebase: you can read the code or ask somebody you trust to read it for you to ensure that there are no back doors and your information is safe.

* **OpenPGP** file format: you can encrypt a file with another tool (gpg for example) implementing the format and open it with EncryptPad and vice versa.

* **Double protection**: randomly generated key files in addition to passphrases.

<div id="when-encryptpad"></div>

## When do I need EncryptPad?

* You have a file containing sensitive information such as account names, passphrases or IDs. It is stored on an unprotected media or you can't control who accesses the file, whether it is located on a computer at work, a laptop while on the move, a memory stick or a cloud drive.

* You need to send an encrypted file to somebody with whom you prearranged a shared secret (a passphrase or a key file). In this case, you need to exchange the secret personally (not via an accessible Internet protocol) for the protected file to be decrypted by the recipient.

* You store or receive a file and need to ensure that it has not been tampered with or corrupted during transmission. EncryptPad uses SHA-1 hashing algorithm to verify the data's integrity.

* You need protection against a brute force attack in case your storage gets in somebody's hands. EncryptPad allows to generate a key and store it separately from encrypted information. The unwanted person would need two secrets to open an encrypted file: the passphrase and the key. Consider this example: you store your encrypted file on a memory stick, and protect it with a passphrase. In addition to that, you protect the file with a file key and store the key on computers where you open the file. If the memory stick is lost, the passphrase is not enough to decrypt your information. The key file is also needed and it is not on the memory stick.

<div id="when-can-i-not"></div>

## When can I not use EncryptPad?

* You need to send a file to somebody with whom you have **not prearranged a shared secret** (a passphrase or a key file). In this case, you need asymmetric encryption with public and private keys. Fortunately, there are many convenient tools suitable for the task. 

* You are on public transport or a common area where **somebody can see your screen**.

* EncryptPad is not effective on a computer infected with spyware or a virus. Do not use it on a **public, shared or compromised computer** if you do not trust its safety.

* **IMPORTANT**: Before using EncryptPad ensure that it is legal in your country to use encryption ciphers that EncryptPad provides. You may find useful information at [cryptolaw.org](http://www.cryptolaw.org/).

* **IMPORTANT**: If you forgot your passphrase or lost a key file, there is nothing that can be done to open your encrypted information. There are no backdoors in the formats that EncryptPad supports. EncryptPad developers take no responsibility for corrupted or invalid files in accordance with the license.

<div id="file-types"></div>

## File types

The format is determined by an extension of a file. Main extensions of encrypted files are GPG and EPD.

<div id="gpg"></div>

### GPG

This file type conforms to OpenPGP format and it is compatible with other OpenPGP tools. Use it if you need to open a file where EncryptPad is not available. The format does not support double protection (key file + passphrase). So you need to choose between key file or passphrase and cannot use both. In addition, it cannot store file key path in the encrypted file. It means that every time you open a file encrypted with a key file, the application will ask you which key file to use.

<div id="epd"></div>

### EPD

EncryptPad specific format. Other OpenPGP software will not be able to open it unless the file was only protected with a passphrase. If passphrase only protection was used, the file is effectively a GPG file (see GPG section above). However, when a key file protection is involved, it is a GPG file in a [WAD](https://en.wikipedia.org/wiki/Doom_WAD) container. See the following chapter for details.

<div id="feature-support"></div>

### Feature support

<table style="border: 1px solid black">
<tr>
<th>Type</th><th>Feature</th><th>Supported</th><th>Key file path\*</th><th>OpenPGP compatible</th><th>File format</th>
</tr>
<tr><td>GPG</td><td>Passphrase</td><td>yes</td><td>n/a</td><td>yes</td><td>OpenPGP file</td></tr>
<tr><td>GPG</td><td>Key file</td><td>yes</td><td>no</td><td>yes</td><td>OpenPGP file</td></tr>
<tr><td>GPG</td><td>Key file and passphrase</td><td>no</td><td>n/a</td><td>n/a</td><td>n/a</td></tr>
<tr><td>EPD</td><td>Passphrase</td><td>yes</td><td>n/a</td><td>yes</td><td>OpenPGP file</td></tr>
<tr><td>EPD</td><td>Key file</td><td>yes</td><td>yes</td><td>no</td><td>Nested: WAD/OpenPGP</td></tr>
<tr><td>EPD</td><td>Key file and passphrase</td><td>yes</td><td>yes</td><td>no</td><td>Nested: OpenPGP/WAD/OpenPGP</td></tr>
</table>

\* Key file location is persisted in the header of an encrypted file so the user does not need to specify it when decrypting.

<div id="key-file"></div>

## What is an EncryptPad key file?
In symmetric encryption the same sequence is used to encrypt and decrypt data. The user or another
application usually provides this sequence in the form of an entered passphrase or a file. In addition to
entered passphrases, EncryptPad generates files with random sequences called "key files".

When the user creates a key file, EncryptPad generates a random sequence of bytes, asks the
user for a passphrase, encrypts the generated sequence and saves it to a file.

The format of the file is OpenPGP. Other OpenPGP implementations can also create and 
open EncryptPad key files as below shell commands demonstrate.

When EncryptPad generates a new key file, it is roughly equivalent to the following `gpg2` command.

    pwmake 1024 | gpg2 -c --armor --cipher-algo AES256 > ~/.encryptpad/foo.key

`pwmake` generates a random sequence, which `gpg2` in-turn encrypts. It will ask for the
passphrase to encrypt the sequence.

When you use this key to encrypt `test3.txt`, the equivalent `gpg` command is below:

    gpg2 --decrypt ~/.encryptpad/foo.key \
    | gpg2 --passphrase-fd 0 --batch -c --cipher-algo AES256 \
    -o /tmp/test3.txt.gpg /tmp/test3.txt

The first `gpg2` process decrypts `foo.key` and directs it to descriptor 0 of the second process
through a pipe. `gpg2` reads the sequence from the descriptor with `--passphrase-fd 0`.

When EncryptPad opens the encrypted file protected with `foo.key`, the equivalent `gpg` commands are:

    gpg2 --decrypt ~/.encryptpad/foo.key \
    | gpg2 --passphrase-fd 0 --batch --decrypt \
    -o /tmp/test4.txt /tmp/test3.txt.gpg

As you see, other OpenPGP implementations can also use EncryptPad keys.

<div id="epd-file-format"></div>

## EPD file format when encrypting with a key

There are three different structures a saved file can have depending on protection mode:

1. **Passphrase only** (passphrase is used to protect a file but no keys are specified). The file is an ordinary OpenPGP file.

2. **Key only** (passphrase is not set but a key file is used for protection). The file is a WAD file. [WAD](https://en.wikipedia.org/wiki/Doom_WAD) is a simple format for combining multiple binary files in one. You can open a WAD file in [Slade](http://slade.mancubus.net/). It contains two files internally: 
    * OpenPGP file encrypted with the key
    * `__X2_KEY` is a plain text file containing the path to the key if "Persistent key location in the encrypted file" is enabled. Otherwise, it has zero length.

3. **Protected with passphrase and key**. The resulting file is an OpenPGP file containing a WAD file as explained in 2.

<div id="use-curl"></div>

## Use CURL to automatically download keys from a remote storage

If **[CURL](http://curl.haxx.se/)** URL is specified in **Key File Path** field in the **Set Encryption Key** dialogue, EncryptPad will attempt to start a curl process to download the key from a remote host. If you want to use this feature, you need to set the path to the CURL executable in the EncryptPad settings. 

Consider this use case scenario: you travel with your laptop and open an encrypted file on the laptop. If you protect the file with a passphrase and a key and your laptop is lost or stolen, the perpetrator will be able to make a brute force attack on your file because the key is also stored on the laptop. To avoid this, EncryptPad takes the following steps:

1. Encrypts the plain text file with the key
2. Copies the encrypted file into a WAD file together with the unencrypted HTTPS or SFTP URL to the key file containing authentication parameters.
3. Encrypts the WAD file from point 2 with the passphrase. 

If this file gets into the hands of a wrongdoer, he or she will need to brute force the passphrase first to be able to obtain the key URL and the authentication parameters. Since a brute force attack takes a lot of time, the user will be able to remove the key or change the authentication so the previous parameters become obsolete.

<div id="known-weaknesses"></div>

## Known weaknesses

* EncryptPad stores unencrypted text in memory. If a memory dump is automatically taken after a system or application crash or some of the memory is saved to a swap file, the sensitive information will be present on the disk. Sometimes it is possible to configure an operating system not to use a dump and swap files. It is a good practice to close EncryptPad when not in use.

<div id="command-line-interface"></div>

## Command line interface

### encryptcli
<div id="command-line-encryptcli"></div>

**encryptcli** is the executable to encrypt / decrypt files in command line. Run it without arguments to see available parameters. Below is an example of encrypting a file with a key:

    # generate a new key and protect it with the passphrase "key".
    # --key-pwd-fd 0 for reading the key passphrase from descriptor 0
    echo -n "key" | encryptcli --generate-key --key-pwd-fd 0 my_key.key

    # encrypt plain_text.txt with my_key.key created above.
    # The key passphrase is sent through file descriptor 3
    cat plain_text.txt | encryptcli -e --key-file my_key.key \
    --key-only --key-pwd-fd 3 -o plain_text.txt.gpg 3< <(echo -n "key")

### encryptpad
<div id="command-line-encryptpad"></div>

**encryptpad** is the GUI executable. It has the command line parameters below:

    `--lang` - to enforce the language for the GUI

    `--log-file` - specify the log file for diagnostics

    `--log-severity` - log severity can be one of the following list: none, fatal, error, warning, info, debug, verbose

<div id="installing"></div>

## Installing EncryptPad

<div id="portable-exe"></div>

### Portable executable

Portable binaries are available for Windows and macOS. They can be copied on a memory stick or
placed on a network share.

<div id="install-on-arch"></div>

### Arch Linux

Use fingerprints to receive gpg keys for EncryptPad and Botan.

    gpg --recv-key 621DAF6411E1851C4CF9A2E16211EBF1EFBADFBC
    gpg --recv-key 634BFC0CCC426C74389D89310F1CFF71A2813E85

Install the AUR packages below:

- [botan-stable](https://aur.archlinux.org/packages/botan-stable/)<sup><small>AUR</small></sup>
- [encryptpad](https://aur.archlinux.org/packages/encryptpad/)<sup><small>AUR</small></sup>

`pacaur` installs `botan-stable` automatically as `encryptpad` dependency.

<div id="install-on-ubuntu"></div>

### Ubuntu or Linux Mint via PPA

Alin Andrei from [**webupd8.org**](http://webupd8.org) kindly created EncryptPad packages for
several distributions. See instructions below on how to install them.

#### Installation

Use the commands below to install the packages.

    sudo add-apt-repository ppa:nilarimogard/webupd8
    sudo apt update
    sudo apt install encryptpad encryptcli

#### Integrity verification procedure

Below are steps to verify the SHA-1 hashes of the source files in [Launchpad webupd8 PPA](https://launchpad.net/~nilarimogard/+archive/ubuntu/webupd8/+packages) used for building the packages. Ideally, you need to be familiar with the PPA concepts.

1\. Download one of the `changes` files below depending on your distribution. The package version was 0.3.2.5 at the moment of writing. Please replace it with the latest version you are installing.

- Yakkety

        wget https://launchpadlibrarian.net/282249531/encryptpad_0.3.2.5-1~webupd8~yakkety1_source.changes

- Xenial

        wget https://launchpadlibrarian.net/282249418/encryptpad_0.3.2.5-1~webupd8~xenial1_source.changes

- Vivid

        wget https://launchpadlibrarian.net/282249098/encryptpad_0.3.2.5-1~webupd8~vivid1_source.changes

- Trusty

        wget https://launchpadlibrarian.net/282247738/encryptpad_0.3.2.5-1~webupd8~trusty1_source.changes

2\. Download the tarball with the verified "changes" files and its signature:

    wget https://github.com/evpo/EncryptPad/releases/download/v0.3.2.5\
    /encryptpad0_3_2_5_webupd8_ppa_changes.tar.gz

    wget https://github.com/evpo/EncryptPad/releases/download/v0.3.2.5\
    /encryptpad0_3_2_5_webupd8_ppa_changes.tar.gz.asc

3\. Receive and verify the `EncryptPad Release` key:

    gpg --recv-key 634BFC0CCC426C74389D89310F1CFF71A2813E85

4\. Verify the signature on the tarball:

    gpg --verify encryptpad0_3_2_5_webupd8_ppa_changes.tar.gz.asc

5\. Extract the content:

    tar -xf encryptpad0_3_2_5_webupd8_ppa_changes.tar.gz

6\. Compare the "changes" file for your distribution with the file from step 1. The SHA hashes should match.

    diff encryptpad_0.3.2.5-1~webupd8~yakkety1_source.changes \
    encryptpad0_3_2_5_webupd8_ppa_changes/encryptpad_0.3.2.5-1~webupd8~yakkety1_source.changes

<div id="compile-on-windows"></div>

## Compile EncryptPad on Windows

<div id="prerequisites"></div>

### Prerequisites

1. [**Qt framework**](http://www.qt.io/download-open-source/) based on MingW 32 bit (the latest build has been tested with Qt 5.10.1).
2. MSYS: you can use one bundled with [**Git For Windows**](http://git-scm.com/download/win). You probably use Git anyway.
3. Python: any recent version will work.

<div id="steps"></div>

### Steps

1. Modify the session **PATH** environment variable to include the Qt build toolset and Python. **mingw32-make**, **g++**, **qmake**, **python.exe** should be in the global search path in your Git Bash session. I personally modify bash.bashrc and add a line like `PATH=/c/Python35-32:/c/Qt/5.10.1/mingw53_32/bin:/c/Qt/Tools/mingw530_32/bin:/c/MinGW/msys/1.0/bin:/bin` not to pollute the system wide PATH variable.

2. Extract the EncryptPad source files to a directory.

3. Run **configure.py --help** script to see available options. To build everything:

    ./configure.py --cpu x86 --os mingw --static
    make

The configure command will always work if your console is running with administrative privileges. If you don't want to run as administrator, add `--link-method hardlink` to the options.
If the build is successful, you should see the executable **./bin/release/encryptpad.exe**

Note that if you want EncryptPad to work as a single executable without dlls, you need to build Qt framework yourself statically. It takes a few hours. There are plenty of instructions on how to do this in the Internet. The most popular article recommends using a PowerShell script. While it is convenient and I did it once, sometimes you don't want to upgrade your PowerShell and install heavy dependencies coming with it. So the next time I had to do that, I read the script and did everything manually. Luckily there are not too many steps in it.

<div id="compile-on-macos"></div>

## Compile EncryptPad on macOS

You need to install Qt 5, Python and run:

    export PATH=$HOME/Qt/5.12.11/clang_64/bin/:$PATH
    ./configure.py --ldflags "-mmacosx-version-min=11.0" --cxxflags "-mmacosx-version-min=11.0"
    make

Change the Qt path and replace the minimal macOS versions as needed. The command will work without them but the result will be limited to the current version.

<div id="compile-on-linux"></div>

## Compile EncryptPad on Linux

<div id="build-on-fedora"></div>

### Fedora

Install dependencies and tools:

    dnf install gcc make qt5-qtbase-devel gcc-c++ python libstdc++-static glibc-static botan2-devel bzip2-devel zlib-devel

Open the EncryptPad directory:

    ./configure.py
    make
    sudo make install

<div id="build-on-ubuntu"></div>

### Ubuntu

Install dependencies and tools:

    apt-get install qt5-default qtbase5-dev gcc g++ make python pkg-config zlib1g-dev libbotan-2-dev libbz2-dev

Open the EncryptPad source directory:

    ./configure.py
    make
    sudo make install

<div id="build-on-debian"></div>

### Debian

Install dependencies and tools:

    apt-get install qtbase5-dev gcc g++ make python3 zlib1g-dev pkg-config libbotan-2-dev libbz2-dev

Open the EncryptPad source directory:

    python3 ./configure.py
    make
    sudo make install

<div id="build-on-opensuse"></div>

### openSUSE

Install dependencies and tools:

    zypper install gcc gcc-c++ make python pkg-config zlib-devel libqt5-qtbase-devel libbotan-devel libbz2-devel

Open the EncryptPad source directory:

    ./configure.py
    make
    sudo make install

<div id="build-on-archlinux"></div>

### Archlinux

Install dependencies and tools:

    pacman -S --needed base-devel
    pacman -S qt5-base python botan zlib bzip2

Open the EncryptPad source directory:

    ./configure.py
    make
    sudo make install

<div id="build-on-freebsd"></div>

### FreeBSD

Install dependencies and tools:

    pkg install python pkgconf botan2 qt5

Open the EncryptPad source directory:

    ./configure.py
    make

<div id="build-on-voidlinux"></div>

### Void Linux

Install dependencies and tools: 
	
	sudo xbps-install base-devel qt5-devel python3 botan-devel bzip2-devel libzip-devel

Open the EncryptPad source directory:

    ./configure.py
    sudo make install
	
<div id="portable-mode"></div>

## Portable mode

EncryptPad checks the executable directory for a sub-directory called `encryptpad_repository`. If exists, it is used for key files and settings. The directory `.encryptpad` in the user's profile is then ignored. The EncryptPad executable and `encryptpad_repository` can both be copied to a removable media and used on multiple computers. It should be noted that keeping encrypted material with the key files on the same removable media is less secure. Separate them if possible.

<div id="fakevim-mode"></div>

## FakeVim mode

FakeVim mode lets edit files with Vim-like interface.

To enable the mode:

1. open Settings... / Preferences ...
2. Set "Enable FakeVim"
3. Restart EncryptPad

To configure FakeVim create and edit the file at the location below:

Linux and macOS:

    ~/.encryptpad/vimrc

On Windows in the user profile directory:

    _encryptpad/vimrc

You can find more information about FakeVim interface at [FakeVim library web page](https://github.com/hluk/FakeVim)

<div id="fakevim-input-output"></div>
### FakeVim: input and output commands

The ex mode supports commands to read and write files. The input and output commands are integrated with the following EncryptPad operations:

    :r <file> - File / Open...

    :w - File / Save

    :w <file> - File / Save As...

    :q - File / Exit

The combinations of the above commands are also supported:

    :wq
    :wq <file>

Vim + register integrates with the system clipboard. You can also add the below line to the vimrc file to integrate the unnamed register with the system clipboard:

    set clipboard=unnamedplus

<div id="passphrases-in-memory"></div>

## Does EncryptPad store passphrases in the memory to reopen files?
No, it does not. After being entered, a passphrase and random salt are hashed with an S2K algorithm. The result is used as the encryption key to encrypt or decrypt the file. A pool of these S2K results is generated every time the user enters a new passphrase. It allows to save and load files protected with this passphrase multiple times without having the passphrase. The size of the pool can be changed in the Preferences dialogue. The latest version at the moment of writing has this number set to 8 by default. It means that you can save a file 8 times before EncryptPad will ask you to enter the passphrase again. You can increase this number but it will have an impact on the performance because S2K algorithms with many iterations are slow by design.

<div id="acknowledgements"></div>

## Acknowledgements

EncryptPad uses the following frameworks and libraries:

1. [**Qt Framework**](http://www.qt.io/)
2. [**Botan**](http://botan.randombit.net/)
3. [**stlplus**](http://stlplus.sourceforge.net/)
5. [**Makefiles**](http://stlplus.sourceforge.net/makefiles/docs/)
4. [**zlib**](http://zlib.net/)
6. [**gtest**](http://code.google.com/p/googletest/)
7. [**famfamfam Silk iconset 1.3**](http://www.famfamfam.com/lab/icons/silk/)
8. [**plog**](https://github.com/SergiusTheBest/plog)
9. [**FakeVim**](https://github.com/hluk/FakeVim)

<div id="integrity-verification"></div>

## EncryptPad integrity verification

<div id="openpgp-signing"></div>

### OpenPGP signing and certification authority

All EncryptPad related downloads are signed with the following OpenPGP key.

`EncryptPad (Releases) 2048R/A2813E85` 

`software@evpo.net` 

`Key fingerprint = 634B FC0C CC42 6C74 389D  8931 0F1C FF71 A281 3E85`

I also have a code signing certificate issued by a certification authority (CA). To establish a connection between my CA certificate and the above OpenPGP key, I created an executable signed with the CA certificate containing fingerprints and the OpenPGP key. You can find `ca_signed_pgp_signing_instructions` in downloads. Effectively I created a bridge of trust between my CA certificate and the OpenPGP key.

There is a few reasons why I did not simply use the CA certificate:

1. EncryptPad is based on the OpenPGP standard and promotes it.
2. OpenPGP signing is more flexible.
3. There is no yearly CA certification running cost.

<div id="verification-process"></div>

### Step by step verification process

1. Download packages and their detached OpenPGP signatures.
2. Import the EncryptPad (Releases) key to your GPG keyring.
3. Ensure that it is the valid EncryptPad (Releases) key by checking its fingerprint with `ca_signed_pgp_signing_instructions`.
4. Verify signatures on the downloaded files with GPG.

<div id="license"></div>

## License

EncryptPad is free software: you can redistribute it and/or modify
it under the terms of the [GNU General Public License](http://www.gnu.org/licenses/) as published by
the Free Software Foundation, either version 2 of the License, or
(at your option) any later version.

EncryptPad is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

<div id="contact"></div>

## Contact and feedback

If your question is related to EncryptPad, send it to the mailing list: **encryptpad@googlegroups.com** linked to [the public discussion group](https://groups.google.com/d/forum/encryptpad).

Bug tracker and contributions: [github.com/evpo/EncryptPad/issues](https://github.com/evpo/EncryptPad/issues)

For other matters, please contact Evgeny Pokhilko **software@evpo.net**

[http://www.evpo.net/encryptpad](http://www.evpo.net/encryptpad)
