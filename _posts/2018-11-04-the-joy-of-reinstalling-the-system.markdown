---
layout: post
title:  "The joy of reinstalling the system"
date:   2018-11-04 21:41:00 -0300
---

It's curious how joyful is to reinstalling all your OS and dependencies. It's like
getting a new toy, except the part that you need to reconfigure everything.

To help on that matter you can share your configuration through [open source repos][dot-files], or having them
stored in a safe place. The last option is difficult to archive without having to trust on
third party companies like Apple, Google or Dropbox. Fortunately we have open source projects that
solve the problem of encrypting your data (arguably) more safely.

## Encrypting credentials

To encrypt your data safely, you can use a piece of software like [VeraCrypt][veracrypt], which has the main
goal of creating virtual encrypted disks. The idea of VeraCrypt is to mount the disk in a point
that you can transfer data back and forth, and after your job is done only unmount and Veracrypt will
encrypt that disk again.

You can use VeraCrypt to store things like your SSH and GPG keys, also you can store certificates
and other kinds of sensible information.

## Before formatting

Make sure you save your credentials and [export your GPG keys][export-gpg] before everything is erased.
It is also a good time to check your passwords and recovery strategies for main accounts like
your email or Github.

Another point is to prepare your installation. In my case I was reinstalling MacOS, so I had to
[prepare an external drive][prepare-the-drive] and put MacOS Mojave on that.
Of course this is not necessary but it's a good idea to not depend on internet to format and
reinstall your system.

## After installing the new system

This is a good oportunity to list and install only the essential software. In my case I had a list
of a few:

- [Homebrew](https://brew.sh);
- git;
- Firefox;
- Telegram;
- Spotify;
- ITerm2;
- tmux;
- neovim;
- [asdf](https://github.com/asdf-vm/asdf) - a version manager;
- Todoist;
- Docker;
- [Numi](https://numi.io);
- [Typora](https://typora.io);
- BetterSnapTool;
- a password manager;
- [ripgrep](https://github.com/BurntSushi/ripgrep) and [fd](https://github.com/sharkdp/fd);
- [VeraCrypt][veracrypt].

Some of the dependencies of those software were installed using Homebrew and the brew cask command.

### Experimenting new stuff

This time was good because I could simplify my environment and try new things. I changed my default
shell program from [ZSH](https://zsh.org) to [Fish](https://fishshell.com), and I'm very happy with it.

Another experimentation was to replace Vundle with Plug on vim/neovim land.
Plug has some handy features like lazy load of plugins by extension or command, and is more active
in development.

## Summing up

It's great to have a fresh system again! But it's a pain to reconfigure everything from scratch.
So my advise is to keep your config files saved and updated somewhere, in order to have an easy
setup. This way you don't have to fear when reinstalling the system.

[dot-files]: https://github.com/phils/dotfiles
[veracrypt]: https://www.veracrypt.fr/
[export-gpg]: https://www.debuntu.org/how-to-importexport-gpg-key-pair/
[prepare-the-drive]: https://www.imore.com/how-create-bootable-installer-mac-operating-system
