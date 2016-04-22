---
layout: page 
title: VI Tips
excerpt: "VI Tips"
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
<tr><td>/</td><td>Search.n for next, N for previous</td></tr>
<tr><td>?</td><td>Search backwards</td></tr>
<tr><td>:%s/OLD/NEW/g</td><td>Replace all OLD with NEW</td></tr>
<tr><td>dgg</td><td>Removes all lines</td></tr>
<tr><td>:set ic</td><td>set case insesitive for search</td></tr>
<tr><td>:set ft=ruby</td><td>set syntax highlight for ruby</td></tr>
<tr><td>e</td><td>Go to end of the word</td></tr>
<tr><td>b</td><td>Go to the beginning of the word</td></tr>
<tr><td>0</td><td>Beginning of the line</td></tr>
<tr><td>$</td><td>End of the line</td></tr>
<tr><td>SHIFT + H</td><td>High - go to first line</td></tr>
<tr><td>SHIFT + M</td><td>Middle - go to the middle of the file</td></tr>
<tr><td>SHIFT + L</td><td>Low - go to the end of the file</td></tr>
<tr><td>O</td><td>New line below and start editing</td></tr>
<tr><td>SHIFT + O</td><td>New line above and start editing</td></tr>
<tr><td>SHIFT + C</td><td>Remove the line and start editing from the beginning</td></tr>
<tr><td>dw</td><td>Delete word</td></tr>
<tr><td>2dw</td><td>Delete 2 words</td></tr>
<tr><td>V</td><td>Visual mode. e and b select text. c change word, y copy, p paste</td></tr>
<tr><td>U</td><td>Undo</td></tr>
<tr><td>CTRL+R</td><td>Redo</td></tr>
<tr><td>:set paste</td><td>Set mode for pasting</td></tr>
<tr><td>SHIFT + D</td><td>Delete from cursor to end of line</td></tr>
<tr><td>:1,10d</td><td>Delete from line 1 to 10</td></tr>
<tr><td>:1,$d</td><td>Delete all lines</td></tr>
<tr><td>:%d</td><td>Delete all lines</td></tr>
</tbody>
</table>


<h3>.vimrc</h3>
<table class="tftable" border="1">
<tbody>
<tr><th>Command</th><th>Description</th></tr>
<tr><td>:set tabstop=4</td><td>One tab=4 spaces</td></tr>
<tr><td>:set expandtab</td><td>Insert space even if pressed tab</td></tr>
<tr><td>:syntax on</td><td>Syntax highlight</td></tr>
</tbody></table>
