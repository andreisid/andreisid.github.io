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
<tr><td>/</td></tr>     <tr><td>Search.n for next, N for previous</td></tr>
<tr><td>?</td></tr>     <tr><td>Search backwards</td></tr>
<tr><td>:%s/OLD/NEW/g</td></tr>     <tr><td>Replace all OLD with NEW</td></tr>
<tr><td>dgg</td></tr>       <tr><td>Removes all lines</td></tr>
<tr><td>:set ic</td></tr>       <tr><td>set case insesitive for search</td></tr>
<tr><td>:set ft=ruby</td></tr> <tr><td>set syntax highlight for ruby</td></tr>
<tr><td>e</td></tr>     <tr><td>Go to end of the word</td></tr>
<tr><td>b</td></tr>     <tr><td>Go to the beginning of the word</td></tr>
<tr><td>0</td></tr>     <tr><td>Beginning of the line</td></tr>
<tr><td>$</td></tr>     <tr><td>End of the line</td></tr>
<tr><td>SHIFT + H</td></tr> <tr><td>High - go to first line</td></tr>
<tr><td>SHIFT + M</td></tr> <tr><td>Middle - go to the middle of the file</td></tr>
<tr><td>SHIFT + L</td></tr> <tr><td>Low - go to the end of the file</td></tr>
<tr><td>O</td></tr>     <tr><td>New line below and start editing</td></tr>
<tr><td>SHIFT + O</td></tr> <tr><td>New line above and start editing</td></tr>
<tr><td>SHIFT + C</td></tr>     <tr><td>Remove the line and start editing from the beginning</td></tr>
<tr><td>dw</td></tr>        <tr><td>Delete word</td></tr>
<tr><td>2dw</td></tr>       <tr><td>Delete 2 words</td></tr>
<tr><td>V</td></tr>     <tr><td>visual mode. e and b select text. c change word, y copy, p paste</td></tr>
<tr><td>U</td></tr>         <tr><td>Undo</td></tr>
<tr><td>CTRL+R</td></tr>        <tr><td>Redo</td></tr>
<tr><td>:set paste</td></tr>        <tr><td>Set mode for pasting</td></tr>
<tr><td>SHIFT + D</td></tr>     <tr><td>delete from cursor to end of line</td></tr>

.vimrc
--------------------------
:set tabstop=4      #one tab=4 spaces
:set expandtab      #insert space even if pressed tab
</tbody></table>
