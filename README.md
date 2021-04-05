# Useful Commands

This README contains a dump of commands that have helped me greatly, yet somehow, I am never able to recall them and always end up spending 10 minutes Googling for them.

## General System/OS

### `sudo apt-get update`
### `sudo apt-get dist-upgrade`

These two commands above together help to update Ubuntu dependencies.

### `sudo du -hsx dir/* | sort -rh | head -n 20`

Get a summary of disk usage for files in the given `dir`, and list the top 20 (arbitrary) of them, with the largest at the top.

### `ssh-keygen -t ed25519 -C "your_email@example.com"`
### `eval "$(ssh-agent -s)"`
### `ssh-add ~/.ssh/id_ed25519`

These three commands above help to generate a new SSH key, based on [GitHub's instructions](https://docs.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent).
The commands above are for Linux - there are other commands for Mac and Windows.

## Databases

### `vacuumdb --analyze --verbose dbname`

Utility for cleaning a PostgreSQL database, and also generate internal statistics used by the PostgreSQL query optimizer. [Read more here](https://www.postgresql.org/docs/current/app-vacuumdb.html).

## Node & NPM

### `ncu -u`

Requires [npm-check-updates](https://www.npmjs.com/package/npm-check-updates) to be installed globally. It upgrades `package.json` dependencies to the latest versions, ignoring specified versions.

## Swift & XCode

### `rm -rf ~/Library/Caches/CocoaPods Pods ~/Library/Developer/Xcode/DerivedData && pod deintegrate && pod install`

Clears all pods and caches and reinstalls them. May need to specify a project for `pod deintegrate`.

## Miscellaneous

### `gs -o output.png -sDEVICE=png256 -dLastPage=1 -r300 -dBackgroundColor=16#ffffff input.pdf`

Uses [Ghostscript](https://www.ghostscript.com) to get an image of the first page of `input.pdf`. The background colour is filled with white.
