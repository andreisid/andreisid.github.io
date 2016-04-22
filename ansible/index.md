---
layout: page 
title: Ansible quickreference
excerpt: "Python quick reference"
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
<tr><td>ansible -m ping group</td><td></td></tr>
<tr><td>ansible -m setup all</td><td></td></tr>
<tr><td>ansible <hosts> -m setup -a "filter=*address*"</td><td></td></tr>
<tr><td>ansible <hosts> -m setup -a "filter=ansible_dist*"</td><td></td></tr>
<tr><td></td><td></td></tr>
<tr><td></td><td></td></tr>
<tr><td></td><td></td></tr>
<tr><td></td><td></td></tr>

<tr><td>ansible test -u root -m service -a "name=httpd state=restarted"	</td><td> restart a service</td></tr> 
<tr><td>ansible test:test1 -u root -m service -a "name=httpd state=started"	</td><td> run on both test and test1 groups</td></tr>
<tr><td>ansible test:!test1 -u root -m service -a "name=httpd state=started" </td><td> run on all vms that are in test but not in test1</td></tr>
<tr><td>ansible test[0] -u root -m service -a "name=httpd state=started" </td><td> run on first host of the group </td></tr>

<tr><td>ansible test -m setup -u root	 </td><td> get current config of vms in test</td></tr>

<tr><td>ansible <group> -m command -a "/etc/init.d/tomcat7 status" --ask-pass</td><td> get status of process on group of servers</td></tr>
</tbody>
</table>
