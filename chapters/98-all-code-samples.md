# 98. All code samples

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Boot, scheduling, and backups](./16-boot-scheduling-and-backups.md) | [Notes index](../README.md) | [Next: Complete questions and answers](./99-complete-q-and-a.md) |

## Linux and the terminal

Source: [Open chapter](./01-linux-and-the-terminal.md)

### Example 1

~~~~text
command [options] [arguments]
~~~~

### Example 2

~~~~sh
pwd
whoami
uname -srm
date
~~~~

### Example 3

~~~~sh
uname --help
~~~~

### Example 4

~~~~sh
man uname
~~~~

### Example 5

~~~~sh
true
printf 'status: %s\n' "$?"
false
printf 'status: %s\n' "$?"
~~~~

## Filesystem and paths

Source: [Open chapter](./02-filesystem-and-paths.md)

### Example 1

~~~~sh
pwd
ls /etc
ls ..
ls ./Documents
~~~~

### Example 2

~~~~sh
printf 'Home: %s\n' "$HOME"
cd ~
pwd
cd -
pwd
~~~~

### Example 3

~~~~sh
cd "$HOME/Project Files"
ls "$HOME/Project Files"
~~~~

### Example 4

~~~~sh
ls -lah "$HOME"
~~~~

### Example 5

~~~~sh
realpath .
realpath "$HOME/Project Files"
~~~~

## Files and directories

Source: [Open chapter](./03-files-and-directories.md)

### Example 1

~~~~sh
mkdir -p "$HOME/linux-practice/work"
cd "$HOME/linux-practice/work"
touch notes.txt
~~~~

### Example 2

~~~~sh
printf 'Linux practice notes\n' > notes.txt
cp notes.txt notes-copy.txt
mv notes-copy.txt saved-notes.txt
ls -l
~~~~

### Example 3

~~~~sh
mkdir -p project/docs
printf 'Draft\n' > project/docs/readme.txt
cp -a project project-backup
~~~~

### Example 4

~~~~sh
cp -i notes.txt saved-notes.txt
mv -i saved-notes.txt notes.txt
~~~~

### Example 5

~~~~sh
rm -i notes.txt
~~~~

### Example 6

~~~~sh
rm -- -temporary-file
~~~~

### Example 7

~~~~sh
ls *.txt
cp report-?.txt "$HOME/linux-practice/"
~~~~

### Example 8

~~~~sh
mkdir -p "$HOME/linux-practice"/{docs,images,logs}
~~~~

### Example 9

~~~~sh
file notes.txt
stat notes.txt
find "$HOME/linux-practice" -type f -name '*.txt' -print
~~~~

## Reading, searching, and editing text

Source: [Open chapter](./04-reading-searching-and-editing-text.md)

### Example 1

~~~~sh
cat notes.txt
less /etc/services
~~~~

### Example 2

~~~~sh
head -n 10 notes.txt
tail -n 20 notes.txt
tail -f application.log
~~~~

### Example 3

~~~~sh
wc notes.txt
wc -l notes.txt
wc -w notes.txt
~~~~

### Example 4

~~~~sh
grep -n 'error' application.log
grep -i 'warning' application.log
grep -v '^#' settings.conf
~~~~

### Example 5

~~~~sh
grep -r --include='*.conf' 'timeout' ./config
~~~~

### Example 6

~~~~sh
cat > services.txt <<'EOF'
web active 8080
worker paused 0
cache active 6379
EOF

cut -d ' ' -f 1 services.txt
sort services.txt
sort services.txt | uniq
~~~~

### Example 7

~~~~sh
nano notes.txt
~~~~

## Permissions, ownership, and ACLs

Source: [Open chapter](./05-permissions-ownership-and-acls.md)

### Example 1

~~~~sh
ls -l notes.txt
~~~~

### Example 2

~~~~sh
chmod u+x script.sh
chmod g-w shared.txt
chmod o-r private.txt
~~~~

### Example 3

~~~~sh
chmod 640 private.txt
chmod 750 deploy.sh
~~~~

### Example 4

~~~~sh
sudo chown ashish:developers shared.txt
sudo chgrp developers shared.txt
~~~~

### Example 5

~~~~sh
umask
umask 027
touch private.txt
mkdir private-dir
ls -ld private.txt private-dir
~~~~

### Example 6

~~~~sh
getfacl shared.txt
setfacl -m u:alex:r-- shared.txt
getfacl shared.txt
~~~~

## Users, groups, and sudo

Source: [Open chapter](./06-users-groups-and-sudo.md)

### Example 1

~~~~sh
id
id ashish
groups
~~~~

### Example 2

~~~~sh
getent passwd ashish
getent group developers
~~~~

### Example 3

~~~~sh
who
w
~~~~

### Example 4

~~~~sh
sudo systemctl status ssh
sudo -l
~~~~

### Example 5

~~~~sh
sudo adduser sam
sudo usermod -aG developers sam
sudo passwd sam
~~~~

## Processes, jobs, and signals

Source: [Open chapter](./07-processes-jobs-and-signals.md)

### Example 1

~~~~sh
ps
ps -ef
ps -eo pid,ppid,user,stat,comm
~~~~

### Example 2

~~~~sh
pgrep -a ssh
~~~~

### Example 3

~~~~sh
sleep 300 &
process_id=$!
printf 'Started process: %s\n' "$process_id"
ps -p "$process_id" -o pid,stat,cmd
kill -TERM "$process_id"
~~~~

### Example 4

~~~~sh
sleep 300 &
jobs -l
~~~~

## Packages and software

Source: [Open chapter](./08-packages-and-software.md)

### Example 1

~~~~sh
sudo apt update
apt list --upgradable
sudo apt upgrade
~~~~

### Example 2

~~~~sh
apt search curl
apt show curl
sudo apt install curl
curl --version
~~~~

### Example 3

~~~~sh
sudo apt remove curl
~~~~

### Example 4

~~~~sh
sudo dnf check-update
sudo dnf upgrade
dnf search curl
sudo dnf install curl
sudo dnf remove curl
~~~~

### Example 5

~~~~sh
sudo pacman -Syu
pacman -Ss curl
sudo pacman -S curl
sudo pacman -R curl
~~~~

### Example 6

~~~~sh
command -v curl
curl --version
~~~~

## Bash shell fundamentals

Source: [Open chapter](./09-bash-shell-fundamentals.md)

### Example 1

~~~~sh
type cd
type printf
command -v bash
~~~~

### Example 2

~~~~sh
project_name='linux-practice'
printf '%s\n' "$project_name"
~~~~

### Example 3

~~~~sh
export APP_MODE=development
printenv APP_MODE
~~~~

### Example 4

~~~~sh
printf 'Editor: %s\n' "$EDITOR"
~~~~

### Example 5

~~~~sh
name='Sam Lee'
printf 'Hello, %s\n' "$name"
printf '%s\n' '$HOME is literal text'
printf '%s\n' "$HOME"
~~~~

### Example 6

~~~~sh
today=$(date +%F)
printf 'Date: %s\n' "$today"
~~~~

### Example 7

~~~~sh
printf '%s\n' *.md
printf '%s\n' report-?.txt
~~~~

### Example 8

~~~~sh
printf '%s\n' chapter-{01,02,03}.md
~~~~

## Bash scripts and control flow

Source: [Open chapter](./10-bash-scripts-and-control-flow.md)

### Example 1

~~~~bash
#!/usr/bin/env bash
printf 'Hello from Bash\n'
~~~~

### Example 2

~~~~sh
bash hello.sh
~~~~

### Example 3

~~~~sh
chmod u+x hello.sh
./hello.sh
~~~~

### Example 4

~~~~bash
#!/usr/bin/env bash

if [[ $# -ne 1 ]]; then
    printf 'Usage: %s DIRECTORY\n' "$0" >&2
    exit 2
fi

directory=$1
if [[ ! -d $directory ]]; then
    printf 'Directory not found: %s\n' "$directory" >&2
    exit 1
fi

printf 'Reading files from %s\n' "$directory"
exit 0
~~~~

### Example 5

~~~~bash
if [[ -f "$1" ]]; then
    printf 'Regular file\n'
elif [[ -d "$1" ]]; then
    printf 'Directory\n'
else
    printf 'Path does not exist or has another type\n'
fi
~~~~

### Example 6

~~~~bash
case "$1" in
    start) printf 'Starting\n' ;;
    stop) printf 'Stopping\n' ;;
    status) printf 'Checking status\n' ;;
    *) printf 'Choose start, stop, or status\n' >&2; exit 2 ;;
esac
~~~~

### Example 7

~~~~bash
shopt -s nullglob
count=0
for log_file in "$directory"/*.log; do
    count=$((count + 1))
done
printf 'Log files: %d\n' "$count"
~~~~

### Example 8

~~~~bash
print_file_type() {
    local path=$1
    if [[ -f $path ]]; then
        printf '%s: regular file\n' "$path"
    elif [[ -d $path ]]; then
        printf '%s: directory\n' "$path"
    else
        printf '%s: not found\n' "$path"
        return 1
    fi
}

print_file_type "$HOME"
~~~~

### Example 9

~~~~sh
cat > count-logs.sh <<'SCRIPT'
#!/usr/bin/env bash
set -u

if [[ $# -ne 1 ]]; then
    printf 'Usage: %s DIRECTORY\n' "$0" >&2
    exit 2
fi

directory=$1
if [[ ! -d $directory ]]; then
    printf 'Directory not found: %s\n' "$directory" >&2
    exit 1
fi

shopt -s nullglob
count=0
for log_file in "$directory"/*.log; do
    count=$((count + 1))
done

printf 'Found %d log files in %s\n' "$count" "$directory"
SCRIPT

chmod u+x count-logs.sh
bash -n count-logs.sh
./count-logs.sh "$HOME"
~~~~

## Pipes, redirection, and text processing

Source: [Open chapter](./11-pipes-redirection-and-text-processing.md)

### Example 1

~~~~sh
printf 'first line\n' > notes.txt
printf 'another line\n' >> notes.txt
cat notes.txt
~~~~

### Example 2

~~~~sh
find "$HOME" -name '*.conf' -print 2> find-errors.txt
~~~~

### Example 3

~~~~sh
wc -l < notes.txt
~~~~

### Example 4

~~~~sh
ps -ef | grep '[s]sh'
grep -i 'error' application.log | wc -l
~~~~

### Example 5

~~~~bash
set -o pipefail
grep 'ERROR' application.log | sort | uniq -c
~~~~

### Example 6

~~~~sh
cut -d ' ' -f 2 services.txt | sort | uniq -c
~~~~

### Example 7

~~~~sh
grep -i 'warning' application.log | tee warnings.txt
~~~~

### Example 8

~~~~sh
find "$HOME/linux-practice" -type f -name '*.tmp' -print0 |
    xargs -0 -r printf 'Matched: %s\n'
~~~~

## Networking and SSH

Source: [Open chapter](./12-networking-and-ssh.md)

### Example 1

~~~~sh
ip address
ip route
hostname
~~~~

### Example 2

~~~~sh
getent hosts example.com
~~~~

### Example 3

~~~~sh
ping -c 4 example.com
~~~~

### Example 4

~~~~sh
ss -ltn
~~~~

### Example 5

~~~~sh
sudo ss -ltnp
~~~~

### Example 6

~~~~sh
curl -I https://example.com
curl -fsS https://example.com -o /dev/null
~~~~

### Example 7

~~~~sh
ssh ashish@example.com
~~~~

### Example 8

~~~~sh
ssh-keygen -t ed25519 -C "ashish@laptop"
~~~~

### Example 9

~~~~sh
ssh-copy-id ashish@example.com
~~~~

## Storage, filesystems, and mounts

Source: [Open chapter](./13-storage-filesystems-and-mounts.md)

### Example 1

~~~~sh
lsblk -f
df -hT
~~~~

### Example 2

~~~~sh
du -sh "$HOME/Downloads"
du -h --max-depth=1 "$HOME"
~~~~

### Example 3

~~~~sh
sudo mkdir -p /mnt/inspection
sudo mount -o ro /dev/DEVICE /mnt/inspection
find /mnt/inspection -maxdepth 2 -type f -print
sudo umount /mnt/inspection
~~~~

### Example 4

~~~~sh
lsblk -f
sudo findmnt --verify
~~~~

## Services, systemd, and logs

Source: [Open chapter](./14-services-systemd-and-logs.md)

### Example 1

~~~~sh
systemctl status ssh
systemctl list-units --type=service --state=running
systemctl is-enabled ssh
~~~~

### Example 2

~~~~sh
sudo systemctl start ssh
sudo systemctl stop ssh
sudo systemctl restart ssh
sudo systemctl enable ssh
sudo systemctl enable --now ssh
sudo systemctl disable ssh
~~~~

### Example 3

~~~~sh
journalctl -u ssh
journalctl -u ssh --since '1 hour ago'
journalctl -u ssh -f
journalctl -b -p warning
~~~~

### Example 4

~~~~ini
[Unit]
Description=Example application
After=network.target

[Service]
Type=simple
User=linuxapp
WorkingDirectory=/opt/linuxapp
ExecStart=/usr/bin/python3 /opt/linuxapp/app.py
Restart=on-failure

[Install]
WantedBy=multi-user.target
~~~~

### Example 5

~~~~sh
sudo systemctl daemon-reload
sudo systemctl status example.service
~~~~

## Security and troubleshooting

Source: [Open chapter](./15-security-and-troubleshooting.md)

### Example 1

~~~~sh
uptime
free -h
df -h
systemctl --failed
journalctl -p err..alert -b
~~~~

### Example 2

~~~~sh
chmod 700 "$HOME/.ssh"
chmod 600 "$HOME/.ssh/id_ed25519"
~~~~

### Example 3

~~~~sh
sudo ufw status verbose
sudo ufw allow OpenSSH
sudo ufw enable
~~~~

### Example 4

~~~~sh
sudo sshd -t
~~~~

## Boot, scheduling, and backups

Source: [Open chapter](./16-boot-scheduling-and-backups.md)

### Example 1

~~~~sh
systemd-analyze time
systemctl get-default
systemctl list-units --type=target
journalctl -b
~~~~

### Example 2

~~~~text
minute hour day-of-month month day-of-week command
~~~~

### Example 3

~~~~cron
15 2 * * * /home/ashish/bin/backup.sh
~~~~

### Example 4

~~~~sh
systemctl list-timers --all
~~~~

### Example 5

~~~~sh
tar -czf "$HOME/linux-practice-backup.tar.gz" -C "$HOME" linux-practice
tar -tzf "$HOME/linux-practice-backup.tar.gz" | head
~~~~

### Example 6

~~~~sh
mkdir -p "$HOME/restore-test"
tar -xzf "$HOME/linux-practice-backup.tar.gz" -C "$HOME/restore-test"
find "$HOME/restore-test" -maxdepth 3 -type f -print
~~~~

### Example 7

~~~~sh
rsync -a --dry-run "$HOME/linux-practice/" "$HOME/backup/linux-practice/"
~~~~
