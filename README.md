# Blue Sheet

![GitHub last commit](https://img.shields.io/github/last-commit/d3fenderz/blue_sheet?label=last%20update%3A)

Cheat sheet for the Blue Team 🧢

Hopefully, this is not Bull S***!!!

## Disclaimer

I prioritize the simplest commands. Most of the time, you don't need all the things.

While this is a cheat sheet, this is not exhaustive at all. TO BE CONTINUED indefinitely...

![](beback.gif)

## Nmap

These are my favorite [Nmap](https://nmap.org/) commands:

```
# Simple way to enumerate open ports
nmap --open {IP}

# Simple scan for services
nmap -sV {IP}

# Simple UDP + TCP scan
nmap -Pn -sU -sT {IP}
```

However, it's best if you can send the output to a txt file or use the export option `-o` with additional formats to customize the output. For example, `-oG` followed by the path to your output files allows saving all results in a structured format.

## Run executables

### Linux exec

```
chmod +x myexec.sh
./myexec.sh
sh myexec.sh
bash myexec.sh
```

### Windows exec

```
script.bat
binary.exe
script.ps1
```

Just type the path to your exec on the console and press enter.

## Inspect the Network

### Linux network

```
ifconfig
ip add
lsof -i
arp -a
netstat -na | egrep 'LISTEN|ESTABLISH'
```

### Windows network

```
ifpconfig
ifpconfig /all
net view /all
arp -a 
```

## Best filters for Wireshark

### Detecting Nmap or Massscan

The following filter can spot half-open TCP connections that are used to bypass basic detection and logging systems:

```
tcp.flags.syn==1 and tcp.flags.ack==0 and tcp.window_size <= 1024
```

## Review the hardware

### Linux system

```
hostnamectl
```

### Windows info

```
Get-ComputerInfo
```

## Inspect files

### Linux files

```
# files that have been recently modified
ls -lat | less /
lsof -u {USER}

# list dotfiles in sensitive directories
find / -name ".*" -type f ! -path "/proc/*" ! -path "/sys/*" -exec ls -al {} \; 2> /dev/null
```

### Windows `forfiles`

```
# text files that have been recently modified
forfiles /S /M *.txt /C "cmd /c echo @path @file @fdate @ftime"
```

[Source: Stackoverflow](https://stackoverflow.com/a/30321221)

```
# view unsigned files in system32
sigcheck -u -e c:\windows\system32
```

## Change passwords

### Linux passwords

```
# only modify the password for user
passwd {USER}

# unlock password for user
passwd -u {USER}

# delete password for user
passwd -d {USER}
```

### Windows passwords

```
net {USER} *

# if it's a domain account
net {USER} * /{DOMAIN}
```

## Stop processes

### Linux processes

```
ps -aux
ps -aux | grep ^root
kill -9 {PID}
```

### Windows processes

```
tasklist /NH | sort
wmic process {PROCESS} delete
Stop-Process -Name {PROCESS}
```

## Disable services

### Linux services

```
systemctl list-units --type service
systemctl disable {SERVICE}
```

### Windows services

```
sc query
sc stop {SERVICE}
```

## Analyze alware

### Linux malware - inspection

```
strings {FILE} | head -7
strings {FILE} | less
file -i {FILE}
```

### Windows malware - inspection

```
debug {FILE}

# view 250 first bytes of file
hexdump -C -n 250 {FILE}

# check file with Virus Total
sigcheck.exe -vt {FILE}
```

## Analyze Memory

### Linux memory

```
# dump
head /dev/mem | hexdump -C

# analysis
gcore -o {file} {PID}
cat /proc/{PID}/smaps > results.txt
```

Use [Volatility](https://volatility3.readthedocs.io) for analysis.

### Windows memory

Use [Volatility](https://volatility3.readthedocs.io) for analysis.

### Other useful resources

* [Volshell](https://volatility3.readthedocs.io/en/latest/volshell.html): direct introspection and access to all features of the volatility library from within a command line environment
* [Valgrind](https://valgrind.org/): the memcheck tool can analyze memory errors (overflows, leaks)

## Shutdown

### Linux off

```
poweroff
```

### Windows off

```
shutdown /s /t 0
```

## Powershell Commands

[Personal cheat sheet](https://github.com/d3fenderz/powershell_commands)
