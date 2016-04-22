---
layout: page 
title: Ansible quickreference
excerpt: "Python quick reference"
---
> ***Note***: ansible.cfg will be read in order from the following locations: ANSIBLE_CONFIG env variable, current dir, home_dir/.ansible.cfg, /etc/ansible/ansible.cfg

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
<tr><td>ansible -m ping group</td><td>Run ping against all vms in group defined in hosts file</td></tr>
<tr><td>ansible -m setup all</td><td>Run setup module againsta all hosts defined in hosts file</td></tr>
<tr><td>ansible <hosts> -m setup -a "filter=*address*"</td><td>Show all details containint address</td></tr>
<tr><td>ansible <hosts> -m setup -a "filter=ansible_dist*"</td><td>Show distribution</td></tr>
<tr><td>ansible <hosts> -m file -a "path=/etc/fstab"</td><td>Show information of the file	</td></tr>
<tr><td>ansible <host> -s -K -m file -a "path=/tmp/etc state=directory mode=0700 owner=root"</td><td>Create a new folder. -s run as sudo, -K ask sudo pass</td></tr>
<tr><td>ansible <hosts> -s -K -m copy -a "src=/etc/fstab dest=/tmp/etc/fstab"</td><td>Copy a file</td></tr>
<tr><td>ansible <hosts> -s -K -m command -a "/sbin/shutdown -t now"</td><td>Shutdown vms</td></tr>
<tr><td>ansible-doc -l 	</td><td>List available modules</td></tr>
<tr><td>ansible all --list-hosts</td><td>List all hosts defied in your inventory</td></tr>
<tr><td>ansible <hosts> -m ping -i ./hosts</td><td>Overwrite hostsfile</td></tr>
<tr><td>ansible all -m ping	</td><td>Run ping on all hosts in the inventory</td></tr>

<tr><td>ansible <hosts> -s -K -m shell -a 'yum list installed|grep python'	</td><td>Run shell command </td></tr>
<tr><td>ansible local -s -K -m setup --tree /tmp/facts</td><td>Save json in a file  </td></tr>
<tr><td>ansible <hosts> -m setup  -a 'filter=*ipv4*'	</td><td>Get ip addresses</td></tr>
<tr><td>ansible <host> -s -K -m yum  -a 'pkg=links state=installed update_cache=true'</td><td>Install package </td></tr>


<tr><td>ansible test -u root -m service -a "name=httpd state=restarted"	</td><td>Restart a service</td></tr> 
<tr><td>ansible test:test1 -u root -m service -a "name=httpd state=started"	</td><td>Run on both test and test1 groups</td></tr>
<tr><td>ansible test:!test1 -u root -m service -a "name=httpd state=started" </td><td>Run on all vms that are in test but not in test1</td></tr>
<tr><td>ansible test[0] -u root -m service -a "name=httpd state=started" </td><td>Run on first host of the group </td></tr>

<tr><td>ansible test -m setup -u root	 </td><td>Get current config of vms in test</td></tr>

<tr><td>ansible <group> -m command -a "/etc/init.d/tomcat7 status" --ask-pass</td><td>Get status of process on group of servers</td></tr>
</tbody>
</table>
