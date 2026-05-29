# Fix Distrobox Sudo

A bash script to automatically restore broken `sudo` privileges inside Distrobox containers.

If you accidentally alter permissions or get locked out of `sudo` with errors like `sudo: /usr/bin/sudo must be owned by uid 0`, this script runs from your host machine to safely bypass the container's broken environment and reset the necessary system file permissions using Podman.

## Prerequisites

* `podman`
* `distrobox`
* `fzf` (Optional, for an improved interactive menu)

## Installation

1. Create a local binary directory if it does not already exist:

```bash
mkdir -p ~/.local/bin

```

2. Create the script file:

```bash
nano ~/.local/bin/fix-distrobox-sudo

```

3. Paste the provided script into the file and save it.
4. Make the script executable:

```bash
chmod +x ~/.local/bin/fix-distrobox-sudo

```

5. Ensure `~/.local/bin` is in your system's PATH.

## Usage

Run the script from your **host machine** (do not run it from inside the container).

### Interactive Mode

To run the script and select your container from a menu, simply run the command without any arguments:

```bash
fix-distrobox-sudo

```

### Direct Mode

To bypass the menu and fix a specific container directly, pass the container name as an argument:

```bash
fix-distrobox-sudo my-container-name

```

## What it fixes

The script forces a root shell into the target container and resets the ownership and permissions of the following critical files:

* `/usr/bin/sudo`
* `/usr/bin/su`
* `/etc/sudo.conf`
* `/etc/sudoers`
* `/etc/sudoers.d/`

## Disclosure

This script was made with some help from AI. I'll likely be doing some manual refactoring soon to clean things up.
