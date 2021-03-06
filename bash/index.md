---
layout: page 
title: Some Bash
excerpt: "Bash commands"
---
<style type="text/css">
.tftable {font-size:12px;color:#333333;width:100%;border-width: 1px;border-color: #729ea5;border-collapse: collapse;}
.tftable th {font-size:12px;background-color:#acc8cc;border-width: 1px;padding: 8px;border-style: solid;border-color: #729ea5;text-align:left;}
.tftable tr {background-color:#d4e3e5;}
.tftable td {font-size:12px;border-width: 1px;padding: 8px;border-style: solid;border-color: #729ea5;}
.tftable tr:hover {background-color:#ffffff;}
</style>
<table class="tftable" border="1">
<tbody>
<tr><th>Command</th><th>Description</th></tr>
<tr><td>netstat -ntlp</td><td>Shows opened ports</td></tr>
<tr><td>nc &lt;ip&gt; &lt;port&gt; -v</td><td>Test connectivity on specified &lt;ip&gt;:&lt;port&gt;</td></tr>
<tr><td>telnet &lt;ip&gt; &lt;port&gt;</td><td>Test connectivity on specified &lt;ip&gt;:&lt;port&gt;</td></tr>
<tr><td>nc -l &lt;port&gt; &lt; file.txt</td><td>Opens up a port and sends the content of the file to whoever connects to that port</td></tr>
<tr><td>rpm -ql &lt;pack.rpm&gt;</td><td>Shows all files contained by specified RPM file</td></tr>
<tr><td>rpm -qf &lt;file&gt;</td><td>Search what RPM contains the selected file</td></tr>
<tr><td>rpm -qV</td><td>Verify if a RPM was altered after installation</td></tr>
<tr><td>typeset|grep TTY</td><td>Shows the name of the terminal you are logged in</td></tr>
<tr><td>env|grep TTY</td><td>Shows the name of the terminal you are logged in</td></tr>
<tr><td>type &lt;binary&gt;</td><td>Shows the location of a executable file</td></tr>
<tr><td>tcpdump -n -i eth0 tcp port &lt;port&gt;</td><td>Listen all tcp packets coming on a specified port</td></tr>
<tr><td>last</td><td>List of everyone who logged in</td></tr>
<tr><td>w</td><td>Who is currently logged in</td></tr>
<tr><td>rpmbuild –rebuild package.src.rpm</td><td>Rebuild rpm from sources</td></tr>
<tr><td>rpm -Uvh –nomd5 &lt;link&gt;.src.rpm</td><td>Install a src.rpm package</td></tr>
<tr><td>rpmbuild -ba /usr/src/redhat/SPECS/&lt;pachet&gt;.spec</td><td>Compile a spec file</td></tr>
<tr><td>find /location -name “*.txt” -exec grep -l &lt;text&gt; {} \;</td><td>Searches all files containing &lt;text&gt;</td></tr>
<tr><td>ldd &lt;binary&gt;</td><td>Shows all libraries used by a file</td></tr>
<tr><td>lsof &lt;binary&gt;</td><td>Shows all opened files in use by a binary</td></tr>
<tr><td>kill -9 $$</td><td>Kills current shell session without saving in history</td></tr>
<tr><td>strace -o /locatie/fisier.out &lt;comanda&gt;</td><td>Logs strace output</td></tr>
<tr><td>sestatus</td><td>Sows selinux staus</td></tr>
<tr><td>setenforce 0</td><td>Disable selinux</td></tr>
<tr><td>ls | wc -l</td><td>Number of files in a folder</td></tr>
<tr><td>command &amp;&gt; file.txt </td><td>Redirect standard output and standard error to file.txt</td></tr>
<tr><td>command 2&gt;file</td><td>Standard error to file</td></tr>
<tr><td>find /tmp -perm -o=w</td><td>Finds all files that can be written by others</td></tr>
<tr><td>chattr +i &lt;file&gt;</td><td>set Immutable ON. file cannot be edited until removing flag</td></tr>
<tr><td>ssh -R &lt;port_home&gt;:localhost:22 &lt;user&gt;@&lt;ip_home&gt;</td><td>Reverse tunnel from remote location to location &lt;home&gt;</td></tr>
<tr><td>ssh -p &lt;port_home&gt; localhost</td><td>Connect from location &lt;home&gt; to remote location using reverse tunnel</td></tr>
<tr><td>ssh -D 5555 &lt;proxy_host&gt;</td><td>Connect to a host in order to use the connection as a proxy(in browser) Using port 5555</td></tr>
<tr><td>lynx –mime_header http://site.com</td><td>Returns headers</td></tr>
<tr><td>python -m SimpleHTTPServer</td><td>Start a http server in the current location</td></tr>
<tr><td>scp /location/file &lt;user&gt;@&lt;server&gt;:/location/file</td><td>Copy file from one server to another</td></tr>
<tr><td>fuser -m /backup</td><td>See who uses partition /backup</td></tr>
<tr><td>free -m</td><td>Free ram space</td></tr>
<tr><td>mount -t nfs &lt;ip&gt;:/location /mount_point</td><td>mount nfs partition</td></tr>
<tr><td>dos2unix &lt;file&gt;</td><td>Prepare a Windows file for Linux</td></tr>
<tr><td>tail -f &lt;file.log&gt;</td><td>Watch changes on a log file as it gets written</td></tr>
<tr><td>screen</td><td>Start a screen</td></tr>
<tr><td>Ctrl+A+D</td><td>Detach screen</td></tr>
<tr><td>screen -ls</td><td>Show running screens</td></tr>
<tr><td>screen -R</td><td>Reattach screen</td></tr>
<tr><td>screen -x</td><td>Attach to a not detached screen session</td></tr>
<tr><td>Ctrl+R</td><td>Reverse search</td></tr>
<tr><td>df -h</td><td>Free space on HDD</td></tr>
<tr><td>du -sh *</td><td>Show size of all files</td></tr>
<tr><td>dmesg | tail</td><td>Kernel log</td></tr>
<tr><td>grep &lt;word&gt; -ri</td><td>Search a word in all files in a directory. Reverse+ignore case</td></tr>
<tr><td>tar -p –same-owner -cvf /location/file.tar.gz /location/</td><td>Archive folder and preserve rights</td></tr>
<tr><td>read -s -p”Password: ” USER_PASSWORD_VARIABLE; echo</td><td>Shell command to read password into variable</td></tr>
<tr><td>ls -lrt</td><td>List content of folder and sort by date</td></tr>
<tr><td>jobs -l</td><td>Show running jobs with PID</td></tr>
<tr><td>Ctrl+l</td><td>Clear scree</td></tr>
<tr><td>Ctrl+u</td><td>Clear line</td></tr>
<tr><td>Ctrl+w</td><td>Delete last word</td></tr>
<tr><td>ps aux</td><td>List process</td></tr>
<tr><td>test -d &lt;folder&gt; || mkdir &lt;folder&gt;</td><td>Test if folder exists and create it if it doesn’t</td></tr>
<tr><td>export HISTSIZE=10000</td><td>Expand history buffer</td></tr>
<tr><td>uname -a |tee out.txt</td><td>Show output on screen and also write it to file</td></tr>
<tr><td>rpm -q –scripts &lt;RPM&gt;</td><td>Show pre/post install scripts of an installed RPM</td></tr>
<tr><td>netstat -net</td><td>Show established connections</td></tr>
<tr><td>mount -o loop imagine.iso /test</td><td>Mount Iso image</td></tr>
<tr><td>iptables -t nat -nL</td><td>Show redirect rules for iptables</td></tr>
<tr><td>sed s/cookie/brownie/g &lt;cookies.txt &gt;brownie.txt</td><td>Replace all ”cookie” with “brownie” and write output</td></tr>
<tr><td>tcpdump -i eth0 port &lt;port&gt; and host &lt;host&gt;</td><td>Listen all TCP on port and from host</td></tr>
<tr><td>sort -t : -k3,2 /etc/passwd</td><td>Sort all lines by the first 2 letters of the 3rd column. Delimiter is “:”</td></tr>
<tr><td>diff -qr /dir1 /dir2</td><td>Verify if the files from the 2 directories differ</td></tr>
<tr><td>rpm -qlp</td><td>Show the content of a not installed RPM</td></tr>
<tr><td>rpm2cpio &lt;rpm&gt; | cpio -idmv</td><td>Extract the content of a RPM</td></tr>
<tr><td>chage -l &lt;user&gt;</td><td>Expiration date for a user’s password</td></tr>
<tr><td>chage -m 0 -M 99999 -I -1 -E -1 &lt;user&gt;</td><td>Set a user’s password to never expire</td></tr>
<tr><td>iostat</td><td>Shows read writes to partitions to disk</td></tr>
<tr><td>netstat -pantu</td><td>Show established connections wih the PID number</td></tr>
<tr><td>stat &lt;file&gt;</td><td>Show information about a file. Write/read access …</td></tr>
<tr><td>fuser &lt;file&gt;</td><td>Shows what process is using a file. Useful for unmounting partition troubleshooting</td></tr>
<tr><td>iftraf</td><td>Tool for traffic monitoring</td></tr>
<tr><td>lsof|grep delete</td><td>Shows deleted files that are still in use. still filling up space</td></tr>
<tr><td>partprobe</td><td>Update kernel info after partition modifications</td></tr>
<tr><td>vmstat 2 3</td><td>Shows info about ram/swap/io/cpu every 2 seconds 3 times</td></tr>
<tr><td>ps -p $$</td><td>Show running shell</td></tr>
<tr><td>source .bashrc</td><td>Rerun bashrc</td></tr>
<tr><td>!?</td><td>Exit status of the last command</td></tr>
<tr><td>!$</td><td>Parameters of the last command</td></tr>
<tr><td>!!</td><td>Run last command</td></tr>
<tr><td>$#</td><td>Number of parameters for a shell script</td></tr>
<tr><td>$1</td><td>1st parameter of a script</td></tr>
<tr><td>tput setaf 1</td><td>Change font color</td></tr>
<tr><td>sh -x file.sh</td><td>Run in debug mode. Show all steps</td></tr>
<tr><td>arp -na</td><td>Show arp table</td></tr>
<tr><td>ping &lt;ip&gt;;arp</td><td>Shows the mac address of the pinged ip</td></tr>
<tr><td>arping -I &lt;interfata&gt; &lt;ip&gt;</td><td>Shows the mac of the ip</td></tr>
<tr><td>ll |awk ‘{print $4}’</td><td>Print the 4th column</td></tr>
<tr><td>zless &lt;archive&gt;</td><td>Shows compressed text files</td></tr>
<tr><td>bzless &lt;archive&gt;</td><td>Shows compressed text files</td></tr>
<tr><td>showmount -e &lt;nfs server&gt;</td><td>Shows info o a NFS Server</td></tr>
<tr><td>sed ‘s/passwd=[a-f0-9]*/REPLACED PASSWORD/g’ in &gt; out</td><td>Trim out password from a file</td></tr>
<tr><td>ln -s /usr/share/zoneinfo/UTC /etc/localtime</td><td>Set localtime to UTC</td></tr>
<tr><td>cat /etc/services</td><td>Show standard ports</td></tr>
<tr><td>host -t ns domain.com</td><td>Shows NS of a domain</td></tr>
<tr><td>nohup &lt;command/script/..&gt;</td><td>Runs a script detached from he current shell session</td></tr>
<tr><td>alien file.rpm</td><td>Transform a rpm to a deb file</td></tr>
<tr><td>dpkg -i file.deb</td><td>Install a deb file</td></tr>
<tr><td>strace -p &lt;PID&gt; -e trace=network -F -s 5000</td><td>Network activity of a process</td></tr>
<tr><td>vi /etc/security/access.conf</td><td>Deny users to run cronjobs</td></tr>
<tr><td>chage -d 0 &lt;user&gt;</td><td>Force a user to change pass at first login</td></tr>
<tr><td>lspci</td><td>List pci devices</td></tr>
<tr><td>lsusb</td><td>List usb devices</td></tr>
<tr><td>getfacl /folder</td><td>Gets ACL of a folder</td></tr>
<tr><td>setfacl -m u:test:rw /folder</td><td>Allow user test rw on the /folder. Partition needs to be mounted with acl option on</td></tr>
<tr><td>grep -v ^# fisier|grep -v -e “^$”</td><td>Removes comments and white lines and shows the content of a file</td></tr>
<tr><td>:%s/old/new/g</td><td>Find and replace in VI</td></tr>
<tr><td>kill -USR1 &lt;pid&gt;</td><td>Shows the progress of a dd command</td></tr>
<tr><td>vi /etc/nologin</td><td>Deny access to non super user. Show message in file</td></tr>
<tr><td>utmpdump /var/log/wtmp</td><td>Read login log file</td></tr>
<tr><td>cat /proc/cmdline</td><td>Show parameters that kernel loaded at boot</td></tr>
<tr><td>ctrl+x e</td><td>Open VI for a long,complicated command</td></tr>
<tr><td>&lt;space&gt; command</td><td>Do not save in history</td></tr>
<tr><td>alt .</td><td>Paste on cli the argument of the last command</td></tr>
<tr><td>dig +short txt keyword.wp.dg.cx</td><td>Search Wikipedia for word “keyword” over DNS</td></tr>
<tr><td>sshfs &lt;user&gt;@&lt;host&gt;:/path /local_path</td><td>Mount folder through ssh. fusermount -u /local_path for umount</td></tr>
<tr><td>vim -x file</td><td>Add password to a file</td></tr>
<tr><td>grep -B 3 &lt;text&gt; &lt;location&gt;</td><td>Shows the occurrence of &lt;test&gt; plus the 3 rows before. -A after, -C center</td></tr>
<tr><td>pgrep apache</td><td>Shows all pids of an apache progress</td></tr>
<tr><td>Ctrl+&lt;left&gt;</td><td>Moves the cursor a word at a time. works in vi and on the command line.works with right arrow also</td></tr>
<tr><td>Ctrl+k</td><td>Deletes from the end of a line to the cursor.opposite Ctrl+W</td></tr>
<tr><td>rdate -sp &lt;server&gt;</td><td>Sync clock with ntp.</td></tr>
<tr><td>ntpstat</td><td>Checks is the time is synchronized with ntp</td></tr>
<tr><td>hdparm -tT /dev/sda1</td><td>Check disk speed</td></tr>
<tr><td>sshuttle –dns -vvr user@bash.proxy.com 0/0</td><td>Poor man VPN. easy way to secure ALL trafic through ssh</td></tr>
<tr><td>ab -n 100 -c 10 www.website.com</td><td>apache benchmark. sends 100 requests, 10 at a time to stress a server</td></tr>
<tr><td>ipcalc -c &lt;ip&gt;/&lt;netmask&gt;</td><td>Ip calculator</td></tr>
<tr><td>dig @ns0.website &lt;zone&gt; axfr</td><td>Returns all records from a zone</td></tr>
<tr><td>cat ip12 | grep -E -o ‘(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)’</td><td>Returns all ips from a file</td></tr>
<tr><td>:(){ :|: &amp; };:</td><td>Fork bomb</td></tr>
<tr><td>figlet “test”</td><td>Ascii text</td></tr>
<tr><td>ps aux|awk ‘{print $1 $2}’</td><td>Print 1st and 2nd column</td></tr>
<tr><td> sed -i “s/foo/bar/g” file</td><td> Edit the file, replace all occurances of foo with bar</td></tr>
<tr><td> kill -USR1 &lt;pid&gt;</td><td> Shows the progress of a in progress “dd” command. You can find the pid with ps</td></tr>
<tr><td>find ./ -inum number -exec rm -i {} ;</td><td>Deletes a file by its inode</td></tr>
<tr><td>ip addr add 192.168.0.1 dev eth0</td><td>Assign ip address</td></tr>
<tr><td>ip route add 192.168.0.0/23 dev eth0</td><td>Assign route</td></tr>
<tr><td>route add default gw 10.150.84.1</td><td>Add default gateway</td></tr>
<tr><td>yum --showduplicates list <rpm> </td><td>Shows all rpm versions in repo</td></tr>
<tr><td>mail -s "subject" -r "sender@mail.com" receiver@mail.com <<< "text"</td><td>Send mail with return address set</td></tr>
<tr><td>ps -o etime <pid> </td><td>How long ago a process was started</td></tr>
<tr><td>cat << 'EOF'|tee input.sh|bash </td><td>Run commands on separate lines and also add them to script</td></tr>
<tr><td>pkill [part_of_process_name]</td><td>Kills the processes named part_of_process_name even if its not the full name</td></tr>
<tr><td>shopt -s cdspell</td><td>You can change directory even if you misspell the name</td></tr>
<tr><td>cat << EOF >> file.txt</td><td>Start writing a file line by line until you enter EOF</td></tr>
<tr><td>curl wttr.in/london</td><td>Wheather in terminal</td></tr>
<tr><td>path=${1?Error argument..}</td><td>Path receives first argument passed to the script, or Error of no argument</td></tr>
<tr><td>ls *.{sh,py}</td><td>List all shell and python scripts</td></tr>
<tr><td>tr -dc A-Za-z0-9_ < /dev/urandom |head -c12|xargs</td><td>Generate random password</td></tr>
<tr><td>bash | lolcat -a -s 250</td><td>Make your terminal interactive and fun</td></tr>
<tr><td>cat <<EOF > index.html</td><td>Write to file directly from bash</td></tr>
<tr><td>hping3 -c 1 -s 123 -p 80 -S <ip> </td><td>Send one TCP SYN to <ip>:80 from source port 123</td></tr>
<tr><td>ping 0|while read a; do echo `date +%T` $a; done</td><td>Add date in front of a ping</td></tr>
<tr><td>crtl+a	</td><td>Go to begining of the line</td></tr>
<tr><td>crtl+e	</td><td>Go to end of the line</td></tr>
<tr><td>lsof -i -Pn	</td><td>Listening and established connections</td></tr>
<tr><td>ps -eLf</td><td>List running threads</td></tr>
<tr><td>top + 'H'</td><td>List running threads</td></tr>
<tr><td>lscpu</td><td>Processor details. threads/core</td></tr>
<tr><td>yum list installed</td><td>Shows installed packages. Like rpm -qa. Also shows repository that was used</td></tr>
<tr><td>dig NS www.domain.com</td><td>Find nameservers for a certain domain</td></tr>
<tr><td>dig -x <ip></td><td>Reverse DNS search for an ip </td></tr>
<tr><td>tcpdump -nn port 53 -c 100</td><td>Exit exit after first 100 captures disable name and port resolution</td></tr>
<tr><td>dig @[nameserver] [domain] +norecurse</td><td>Get a non cached response from an authoritive DNS Server</td></tr>
<tr><td>dig <domain> +trace</td><td>Traceroute for DNS queries</td></tr>
<ttbody>
</table>
