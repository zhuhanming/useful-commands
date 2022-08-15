# Useful Commands

This README contains a dump of commands that have helped me greatly, yet somehow, I am never able to recall them and always end up spending 10 minutes Googling for them.

## General System/OS

### Update Ubuntu dependencies

```bash
sudo apt-get update
sudo apt-get dist-upgrade
```

These two commands above together help to update Ubuntu dependencies.

### Get disk usage

```bash
sudo du -hsx dir/* | sort -rh | head -n 20
```

Get a summary of disk usage for files in the given `dir`, and list the top 20 (arbitrary) of them, with the largest at the top.

### Generate a new SSH key

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

These three commands above help to generate a new SSH key, based on [GitHub's instructions](https://docs.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent).
The commands above are for Linux - there are other commands for Mac and Windows.

### Create a new superuser account

```bash
adduser username
usermod -aG sudo username
su - username
mkdir ~/.ssh && chmod 700 ~/.ssh
touch ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys
```

These commands above help to create a new superuser account and set up the SSH keys accordingly.

### Flush DNS cache

```bash
sudo dscacheutil -flushcache; sudo killall -HUP mDNSResponder
```

Flushes the DNS cache on Mac.

## Certbot and NGINX

### Create a certificate without affecting NGINX

```bash
sudo certbot certonly -d example.com --nginx
```

Creates a certificate but doesn't touch the NGINX default configuration.

### Link NGINX `sites-enabled`

```bash
sudo ln -s /etc/nginx/sites-available/example.com /etc/nginx/sites-enabled/
```

Links the certificate in `sites-available` to `sites-enabled`.

### Manual Renewal of Certificates

```bash
sudo certbot certonly --manual -d example.com --preferred-challenges dns
```

## Databases

### Vacuum PostgreSQL database

```bash
vacuumdb --analyze --verbose dbname
```

Utility for cleaning a PostgreSQL database, and also generate internal statistics used by the PostgreSQL query optimizer. [Read more here](https://www.postgresql.org/docs/current/app-vacuumdb.html).

## Node & NPM

### Update all dependencies

```bash
ncu -u
npm install # or yarn install
```

Requires [npm-check-updates](https://www.npmjs.com/package/npm-check-updates) to be installed globally. It upgrades `package.json` dependencies to the latest versions, ignoring specified versions.

### Fix audit vulnerabilities for `yarn`

```bash
npx yarn-audit-fix
```

Will install [yarn-audit-fix](https://www.npmjs.com/package/yarn-audit-fix) and run it to fix vulnerabilities detected in the dependencies. Used for yarn projects.

## Poetry

### List outdated top-level dependencies

```bash
poetry show --outdated | grep --file=<(poetry show --tree | grep '^\w' | cut -d' ' -f1 | sed 's/.*/^&\\s/')
```

Credit goes to @Hultner [(see his comment here)](https://github.com/python-poetry/poetry/issues/2684#issuecomment-1076560832).

## Swift & XCode

### Clean pods and caches

```bash
rm -rf ~/Library/Caches/CocoaPods Pods ~/Library/Developer/Xcode/DerivedData && pod deintegrate && pod install
```

Clears all pods and caches and reinstalls them. May need to specify a project for `pod deintegrate`.

## Miscellaneous

### Get first page of a PDF file as an image

```bash
gs -o output.png -sDEVICE=png256 -dLastPage=1 -r300 -dBackgroundColor=16#ffffff input.pdf
```

Uses [Ghostscript](https://www.ghostscript.com) to get an image of the first page of `input.pdf`. The background colour is filled with white.

### Replace word in file names recursively

```bash
find . -name "*sql.xz" -exec bash -c ' mv $0 ${0/beyond-server/sparks}' {} \;
```
